<script lang="ts">
	import { getContext } from 'svelte';
	import { writable } from 'svelte/store';
	import { SvelteFlow, Controls, Background, BackgroundVariant, MiniMap } from '@xyflow/svelte';
	import '@xyflow/svelte/dist/style.css';

	// Initialize nodes and edges as writable stores.
	const nodes = writable([
		{ id: '1', type: 'input', data: { label: 'Input Node' }, position: { x: 0, y: 0 } },
		{ id: '2', type: 'default', data: { label: 'Node' }, position: { x: 0, y: 150 } }
	]);
	const edges = writable([
		{ id: '1-2', type: 'default', source: '1', target: '2', label: 'Edge Text' }
	]);
	const snapGrid: [number, number] = [25, 25];

	// Helper: Validate parsed JSON structure.
	function isValidGraph(graph: any): graph is { nodes: any[]; edges: any[] } {
		return graph && Array.isArray(graph.nodes) && Array.isArray(graph.edges);
	}

	// Reads the file and updates the graph.
	async function handleFile(file: File) {
		console.log('File size (bytes):', file.size);
		try {
			const content = (await file.text()).trim();
			console.log('File content length:', content.length);
			console.log('File content (first 100 chars):', content.slice(0, 100));
			console.log('File content (last 20 chars):', content.slice(-20));

			if (!content) {
				console.error('File content is empty');
				alert('The file appears to be empty.');
				return;
			}

			const parsed = JSON.parse(content);
			console.log('Parsed JSON:', parsed);
			if (isValidGraph(parsed)) {
				nodes.set(parsed.nodes);
				edges.set(parsed.edges);
				console.log('Graph updated from file.');
			} else {
				console.error('Missing required keys in JSON:', parsed);
				alert('Invalid file format. Ensure the file contains "nodes" and "edges".');
			}
		} catch (err) {
			console.error('Error reading/parsing file:', err);
			alert('JSON Syntax error: ' + (err instanceof Error ? err.message : 'Unknown error'));
		}
	}

	// Extracts the File object from the drag event.
	function extractFileFromEvent(event: DragEvent): File | null {
		if (!event.dataTransfer) return null;
		// Try items first.
		if (event.dataTransfer.items) {
			for (let i = 0; i < event.dataTransfer.items.length; i++) {
				if (event.dataTransfer.items[i].kind === 'file') {
					return event.dataTransfer.items[i].getAsFile();
				}
			}
		}
		// Fallback to files.
		return event.dataTransfer.files?.[0] || null;
	}

	async function handleDrop(event: DragEvent) {
		event.preventDefault();
		const file = extractFileFromEvent(event);
		if (!file) {
			console.error('No file detected in drop event.');
			alert('No file found. Please try again.');
			return;
		}

		console.log('Dropped file name:', file.name);
		console.log('File size (bytes):', file.size);
		if (file.size === 0) {
			alert('File appears empty. Check your drag & drop source.');
			return;
		}

		await handleFile(file);
	}

	function handleDragOver(event: DragEvent) {
		event.preventDefault();
	}
	const darkMode = getContext('darkMode') as SvelteStore<any>;
</script>

<div class="flex flex-col items-center space-y-4">
	<!-- File input with modern styling -->
	<input
		type="file"
		accept=".flow.json"
		class="px-4 py-2 border border-gray-300 dark:border-gray-600 rounded shadow-sm
              focus:outline-none focus:ring-2 focus:ring-blue-500
              dark:bg-gray-800 dark:text-gray-200
              file:bg-gray-200 file:text-gray-800
              dark:file:bg-gray-700 dark:file:text-gray-300
              file:rounded file:px-3 file:py-1 file:border-none file:cursor-pointer"
		on:change={(e) => {
			const input = e.target as HTMLInputElement;
			const file = input.files?.[0];
			if (file) handleFile(file);
		}}
	/>

	<!-- Drag & Drop Area -->
	<div
		class="h-[500px] w-full max-w-4xl border-2 border-dashed border-gray-300 dark:border-gray-600 bg-gray-100 dark:bg-gray-900 relative flex items-center justify-center"
		on:drop={handleDrop}
		on:dragover={handleDragOver}
		role="application"
	>
		<p
			class="absolute top-4 left-4 z-10 bg-white dark:bg-gray-800 bg-opacity-80 dark:bg-opacity-60 px-3 py-1 rounded text-sm text-gray-700 dark:text-gray-300 shadow"
		>
			Drop your .flow.json file here to load the graph roadmap.
		</p>

		<SvelteFlow
			{nodes}
			{edges}
			{snapGrid}
			fitView
			colorMode={$darkMode ? 'dark' : 'light'}
			on:nodeclick={(event) => console.log('Node clicked:', event.detail.node)}
		>
			<Controls />
			<Background variant={BackgroundVariant.Dots} />
			<MiniMap />
		</SvelteFlow>
	</div>
</div>
