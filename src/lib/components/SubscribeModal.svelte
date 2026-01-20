<script lang="ts">
	import Modal from "$lib/components/Modal.svelte";
	import { isPro } from "$lib/stores/isPro";
	import IconPro from "$lib/components/icons/IconPro.svelte";
	import IconDazzled from "$lib/components/icons/IconDazzled.svelte";

	interface Props {
		close: () => void;
	}

	let { close }: Props = $props();
</script>

<Modal closeOnBackdrop={false} onclose={close} width="!max-w-[420px] !m-4">
	<div
		class="flex w-full flex-col gap-8 bg-white bg-gradient-to-b to-transparent px-6 pb-7 dark:bg-black dark:from-white/10 dark:to-white/5"
	>
		<div
			class="-mx-6 grid h-48 select-none place-items-center bg-gradient-to-t from-black/5 dark:from-white/10"
		>
			<div class="flex flex-col items-center justify-center gap-2.5 px-8 text-center">
				<div
					class="flex size-14 items-center justify-center rounded-full text-3xl {$isPro
						? 'bg-gradient-to-br from-yellow-500/15 via-orange-500/15 to-red-500/15'
						: 'bg-gradient-to-br from-pink-500/15 from-15% via-green-500/15 to-yellow-500/15'}"
				>
					{#if $isPro}
						<IconDazzled />
					{:else}
						<IconPro classNames="!mr-0" />
					{/if}
				</div>
				<h2 class="text-2xl font-semibold text-gray-900 dark:text-gray-100">
					{$isPro ? "积分用完了" : "需要升级"}
				</h2>
			</div>
		</div>

		<div class="text-gray-700 dark:text-gray-200">
			{#if $isPro}
				<p class="text-[15px] leading-relaxed">
					您已用完所有可用积分。请购买额外积分以继续使用HuggingChat。
				</p>
				<p class="mt-3 text-[15px] italic leading-relaxed opacity-75">
					您的积分可以在其他HF服务和外部应用中通过Inference Providers使用。
				</p>
			{:else}
				<p class="text-[15px] leading-relaxed">
					您已达到消息限制。请升级到Hugging Face PRO以继续使用HuggingChat。
				</p>
				<p class="mt-3 text-[15px] italic leading-relaxed opacity-75">
					您也可以在您喜欢的AI工具中使用PRO积分。
				</p>
			{/if}
		</div>

		<div class="flex flex-col gap-2.5">
			{#if $isPro}
				<a
					href="https://huggingface.co/settings/billing?add-credits=true"
					target="_blank"
					rel="noopener noreferrer"
					class="w-full rounded-xl bg-black px-5 py-2.5 text-center text-base font-medium text-white hover:bg-gray-800 dark:bg-white dark:text-black dark:hover:bg-gray-200"
				>
					购买积分
				</a>
			{:else}
				<a
					href="https://huggingface.co/subscribe/pro?from=HuggingChat"
					target="_blank"
					rel="noopener noreferrer"
					class="w-full rounded-xl bg-black px-5 py-2.5 text-center text-base font-medium text-white hover:bg-gray-800 dark:bg-white dark:text-black dark:hover:bg-gray-200"
				>
					升级到Pro
				</a>
			{/if}
			<button
				class="w-full rounded-xl bg-gray-200 px-5 py-2.5 text-base font-medium text-gray-700 hover:bg-gray-300/80 dark:bg-white/5 dark:text-gray-200 dark:hover:bg-white/10"
				onclick={close}
			>
				稍后再说
			</button>
		</div>
	</div>
</Modal>
