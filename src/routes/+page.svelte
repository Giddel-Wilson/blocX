<script lang="ts">
	import { onMount } from 'svelte';
	import { fade, fly } from 'svelte/transition';
	import { Button } from '$lib/components/ui/button';
	import { Card } from '$lib/components/ui/card';
	import { Avatar } from '$lib/components/ui/avatar';
	import { Input } from '$lib/components/ui/input';
	import { Search, Home, Clock, Box, Settings, LogOut } from 'lucide-svelte';
	import Chart from '$lib/components/chart.svelte';
	import Marquee from '$lib/Marquee.svelte';
	import { ChevronLeft } from 'lucide-svelte';
	import {
		Select,
		SelectTrigger,
		SelectValue,
		SelectContent,
		SelectItem
	} from '$lib/components/ui/select';

	import { cn } from '$lib/utils';
	export let pauseOnHover: boolean = false;
	export let vertical: boolean = false;
	export let repeat: number = 4;
	export let reverse: boolean = false;

	let className: any = '';
	export { className as class };

	let mounted = false;

	const cryptoData = [
		{
			symbol: 'BTC',
			name: 'Bitcoin',
			price: '8442.55',
			change: '+0.2%',
			currency: 'USD',
			icon: '₿',
			color: 'from-orange-400'
		},
		{
			symbol: 'ETH',
			name: 'Ethereum',
			price: '4772.18',
			change: '-2.3%',
			currency: 'USD',
			icon: 'Ξ',
			color: 'from-blue-400'
		},
		{
			symbol: 'LTC',
			name: 'Litecoin',
			price: '3612.65',
			change: '+4.2%',
			currency: 'USD',
			icon: 'Ł',
			color: 'from-gray-400'
		},
		{
			symbol: 'ETH',
			name: 'Ethereum',
			price: '4772.18',
			change: '-2.8%',
			currency: 'USD',
			icon: 'Ξ',
			color: 'from-blue-400'
		},
		{
			symbol: 'BTC',
			name: 'Bitcoin',
			price: '8442.55',
			change: '+0.2%',
			currency: 'USD',
			icon: '₿',
			color: 'from-orange-400'
		}
	];

	let selectedPeriod = 'monthly';

	const marketTrends = [
		{ name: 'BTC', fullName: 'Bitcoin', price: '$8584', change: '2.640', trend: 'up' },
		{ name: 'BNB', fullName: 'BNB', price: '$37202', change: '2.904', trend: 'up' },
		{ name: 'ETH', fullName: 'Ethereum', price: '$77123', change: '1.320', trend: 'up' },
		{ name: 'LTC', fullName: 'Litecoin', price: '$10601', change: '2.140', trend: 'up' },
		{ name: 'ADA', fullName: 'Cardano', price: '$3756', change: '3.978', trend: 'up' },
		{ name: 'CAKE', fullName: 'Pancake', price: '$72650', change: '1.903', trend: 'down' }
	];

	onMount(() => {
		mounted = true;
	});

	import Minus from 'lucide-svelte/icons/minus';
	import Plus from 'lucide-svelte/icons/plus';
	import * as Drawer from '$lib/components/ui/drawer/index.js';

	const data = [
		{
			id: 1,
			goal: 400
		},
		{
			id: 2,
			goal: 300
		},
		{
			id: 3,
			goal: 200
		},
		{
			id: 4,
			goal: 300
		},
		{
			id: 5,
			goal: 200
		},
		{
			id: 6,
			goal: 278
		},
		{
			id: 7,
			goal: 189
		},
		{
			id: 8,
			goal: 239
		},
		{
			id: 9,
			goal: 300
		},
		{
			id: 10,
			goal: 200
		},
		{
			id: 11,
			goal: 278
		},
		{
			id: 12,
			goal: 189
		},
		{
			id: 13,
			goal: 349
		},
		{
			id: 14,
			goal: 180
		},
		{
			id: 15,
			goal: 79
		},
		{
			id: 16,
			goal: 40
		}
	];

	const x = (d: { goal: number; id: number }) => d.id;
	const y = (d: { goal: number; id: number }) => d.goal;

	let goal = 250;

	function handleClick(adjustment: number) {
		goal = Math.max(42, Math.min(400, goal + adjustment));
	}
</script>

<div class="flex h-screen bg-[#13111C]">
	<!-- Sidebar -->
	<aside class="hidden w-16 flex-col items-center border-r border-gray-800 py-6 md:flex">
		<div class="mb-8">
			<div class="flex h-8 w-8 items-center justify-center rounded-lg bg-purple-600">GW</div>
		</div>
		<nav class="flex flex-col items-center gap-6 text-gray-400">
			<Button
				variant="ghost"
				class="h-14 w-14 rounded-xl hover:bg-purple-600/20 hover:text-purple-500"
			>
				<Home class="h-5 w-5" />
			</Button>
			<Button
				variant="ghost"
				class="h-14 w-14 rounded-xl hover:bg-purple-600/20 hover:text-purple-500"
			>
				<Clock class="h-5 w-5" />
			</Button>
			<Button
				variant="ghost"
				class="h-14 w-14 rounded-xl hover:bg-purple-600/20 hover:text-purple-500"
			>
				<Box class="h-5 w-5" />
			</Button>
			<Button
				variant="ghost"
				class="h-14 w-14 rounded-xl hover:bg-purple-600/20 hover:text-purple-500"
			>
				<Settings class="h-5 w-5" />
			</Button>
		</nav>
		<Button
			variant="ghost"
			class="mt-auto h-14 w-14 rounded-xl hover:bg-purple-600/20 hover:text-purple-500"
		>
			<LogOut class="h-5 w-5" />
		</Button>
	</aside>

	<div class="flex-1 overflow-y-auto lg:overflow-x-hidden">
		<!-- Header -->
		<header class="flex items-center justify-between border-b border-gray-800 p-4">
			<Drawer.Root>
				<Drawer.Trigger asChild let:builder>
					<Button
						builders={[builder]}
						variant="ghost"
						class="flex items-center justify-center text-white focus:bg-transparent md:hidden"
					>
						<svg
							xmlns="http://www.w3.org/2000/svg"
							width="24"
							height="24"
							viewBox="0 0 24 24"
							fill="none"
							stroke="currentColor"
							stroke-width="2"
							stroke-linecap="round"
							stroke-linejoin="round"
							class="lucide lucide-menu"
							><line x1="4" x2="20" y1="12" y2="12" /><line x1="4" x2="20" y1="6" y2="6" /><line
								x1="4"
								x2="20"
								y1="18"
								y2="18"
							/></svg
						>
					</Button>
				</Drawer.Trigger>
				<Drawer.Content class="bg-[#13111C]">
					<div class="mx-auto w-full max-w-sm">
						<Drawer.Header>
							<Drawer.Title class="text-gray-300/90">Order Signals</Drawer.Title>
							<Drawer.Description>Set your daily trading goals.</Drawer.Description>
						</Drawer.Header>
						<div class="p-4 pb-0">
							<div class="flex items-center justify-center space-x-2">
								<Button
									variant="outline"
									size="icon"
									class="h-8 w-8 shrink-0 rounded-full bg-transparent text-gray-200"
									on:click={() => handleClick(-10)}
									disabled={goal <= 42}
								>
									<Minus class="h-4 w-4" />
									<span class="sr-only">Decrease</span>
								</Button>
								<div class="flex-1 text-center">
									<div class="text-7xl font-bold tracking-tighter text-gray-200">
										+{goal}
									</div>
									<div class="text-[0.70rem] uppercase text-muted-foreground">Profit/day</div>
								</div>
								<Button
									variant="outline"
									size="icon"
									class="h-8 w-8 shrink-0 rounded-full bg-transparent text-gray-200"
									on:click={() => handleClick(10)}
									disabled={goal >= 400}
								>
									<Plus class="h-4 w-4" />
									<span class="sr-only">Increase</span>
								</Button>
							</div>
							<div class="mt-3 h-[120px]">
								<Chart type="line" color="from-purple-400" />
							</div>
						</div>
						<Drawer.Footer>
							<Button class="border border-gray-400/70">Report Progress</Button>
							<Drawer.Close asChild let:builder>
								<Button builders={[builder]} variant="outline">Cancel</Button>
							</Drawer.Close>
						</Drawer.Footer>
					</div>
				</Drawer.Content>
			</Drawer.Root>

			<Button
				variant="ghost"
				class="hidden h-10 w-10 items-center justify-center rounded-full bg-gray-100 bg-opacity-10 hover:bg-gray-200 hover:bg-opacity-20 md:flex"
			>
				<span>
					<ChevronLeft class="h-4 w-4 text-gray-400" />
				</span>
			</Button>
			<span class="flex items-center gap-2 font-medium text-white">Home</span>
			<div class="flex items-center gap-4">
				<div class="relative hidden md:block">
					<Input
						type="search"
						placeholder="Search"
						class="w-64 rounded-full border-gray-800 bg-gray-900/50 pl-14"
					/>
					<Search class="absolute left-3 top-1/2 h-4 w-4 -translate-y-1/2 text-gray-400" />
				</div>
				<Button variant="ghost" class="h-10 w-10 rounded-full border border-gray-400">
					<span class="sr-only">Notifications</span>
					<div class="flex h-8 w-8 items-center justify-center rounded-full text-gray-400">
						<svg
							xmlns="http://www.w3.org/2000/svg"
							width="16"
							height="16"
							viewBox="0 0 24 24"
							fill="none"
							stroke="currentColor"
							stroke-width="2"
							stroke-linecap="round"
							stroke-linejoin="round"
							class="lucide lucide-bell"
							><path d="M6 8a6 6 0 0 1 12 0c0 7 3 9 3 9H3s3-2 3-9" /><path
								d="M10.3 21a1.94 1.94 0 0 0 3.4 0"
							/></svg
						>
					</div>
				</Button>
				<Button
					variant="ghost"
					class="h-10 w-10 rounded-full bg-gray-100 bg-opacity-10 hover:bg-gray-200 hover:bg-opacity-20"
				>
					<span class="sr-only">Profile</span>
					<div class="flex h-8 w-8 items-center justify-center rounded-full text-gray-400">
						<svg
							xmlns="http://www.w3.org/2000/svg"
							width="16"
							height="16"
							viewBox="0 0 24 24"
							fill="none"
							stroke="currentColor"
							stroke-width="2"
							stroke-linecap="round"
							stroke-linejoin="round"
							class="lucide lucide-user"
							><path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2" /><circle
								cx="12"
								cy="7"
								r="4"
							/></svg
						>
					</div>
				</Button>
			</div>
		</header>

		<!-- Main Content -->
		<main class="p-6">
			<!-- Hero Section -->
			<div class="mb-8 flex flex-col gap-6 md:flex-row">
				<Card
					class="relative flex-1 overflow-hidden bg-gradient-to-br from-purple-700 to-purple-900 p-8"
				>
					{#if mounted}
						<div class="relative z-20" in:fly={{ y: 20, duration: 1400 }}>
							<div class="mb-2 text-sm text-purple-300">ETHEREUM 2.0</div>
							<h1 class="mb-2 text-3xl font-bold text-white">Your Gateway<br />into Blockchain</h1>
							<p class="mb-4 text-purple-200">
								blocX is a blockchain platform.<br />We make blockchain accessible.
							</p>
							<Button class="bg-[#2D2645] text-white hover:bg-[#372D52]">Learn More</Button>
						</div>
						<!-- 3D Elements -->
						<div class="absolute right-0 top-0 h-full w-1/2">
							<div
								class="animate-float-1 absolute right-20 top-14 h-20 w-20 rotate-45 transform rounded-full bg-gradient-to-br from-cyan-400 to-blue-500"
							></div>
							<div
								class="animate-float-2 absolute right-40 top-20 h-16 w-16 -rotate-12 transform rounded-lg bg-gradient-to-br from-purple-400 to-pink-500"
							></div>
							<div
								class="animate-float-3 absolute bottom-20 right-14 h-8 w-24 rotate-12 transform rounded-full bg-gradient-to-r from-green-400 to-emerald-500"
							></div>
						</div>
					{/if}
				</Card>

				<Card class="flex-1 bg-[#1F1B2E] p-6">
					<div class="mb-4 flex items-center gap-2">
						<div class="flex items-center gap-2">
							<div class="h-3 w-3 rounded-full bg-white"></div>
							<span class="text-sm text-gray-400">ETH/USD</span>
						</div>
						<div class="ml-auto flex gap-1">
							<Button variant="ghost" size="sm" class="h-6 px-2 py-1 text-xs text-gray-400"
								>1D</Button
							>
							<Button
								variant="ghost"
								size="sm"
								class="h-6 bg-purple-600/20 px-2 py-1 text-xs text-purple-400">1W</Button
							>
							<Button variant="ghost" size="sm" class="h-6 px-2 py-1 text-xs text-gray-400"
								>1M</Button
							>
						</div>
					</div>
					<div class="h-48">
						<Chart type="area" />
					</div>
				</Card>
			</div>

			<!-- Crypto Cards -->
			<div class="flex gap-4 overflow-x-auto pb-0">
				<Marquee pauseOnHover class="[--duration:20s]">
					<div class="mb-6 flex gap-4 overflow-x-auto pb-4">
						{#each cryptoData as crypto}
							<Card class="relative w-64 flex-none overflow-hidden bg-[#1F1B2E] p-4">
								<div class="mb-2 flex items-center gap-2">
									<div
										class="h-6 w-6 rounded-full bg-gradient-to-br {crypto.color} flex items-center justify-center to-transparent font-medium"
									>
										{crypto.icon}
									</div>
									<span class="text-gray-200">{crypto.symbol}/</span>
									<span class="text-gray-400">{crypto.currency}</span>
									<span
										class="ml-auto text-sm {crypto.change.startsWith('+')
											? 'text-green-500'
											: 'text-red-500'}">{crypto.change}</span
									>
								</div>
								<div class="mb-2 text-2xl font-bold text-gray-200">{crypto.price}</div>
								<div class="h-16">
									<Chart
										type="line"
										color={crypto.change.startsWith('+') ? '#22c55e' : '#ef4444'}
									/>
								</div>
							</Card>
						{/each}
					</div>
				</Marquee>
			</div>

			<!-- Market Overview and Quick Transfer -->
			<div class="flex flex-col gap-6 lg:flex-row">
				<!-- Market Overview -->
				<Card class="flex-1 rounded-2xl bg-[#1F1B2E]/80 backdrop-blur-sm">
					<div class="flex items-center justify-between p-6 pb-4">
						<h2 class="text-base font-medium text-white">Market Overview</h2>
						<select
							bind:value={selectedPeriod}
							class="h-8 w-28 rounded border-0 bg-[#2D2645] px-2 text-sm text-white focus:outline-none focus:ring-1 focus:ring-purple-500"
						>
							<option value="monthly">Monthly</option>
							<option value="weekly">Weekly</option>
							<option value="daily">Daily</option>
						</select>
					</div>
					<div class="h-[250px] px-6">
						<Chart type="multi" />
					</div>
				</Card>

				<!-- Quick Transfer -->
				<Card class="w-full rounded-2xl bg-[#1F1B2E]/80 p-6 backdrop-blur-sm lg:w-[280px]">
					<h2 class="mb-6 text-base font-medium text-white">Quick Transfer</h2>
					<div class="mb-8 flex items-center gap-3">
						<Avatar class="h-14 w-14 border-2 border-purple-500/50">
							<img
								src="https://i.pinimg.com/474x/ec/be/26/ecbe2627364dfdec105805e1aa69c749.jpg?enhanced"
								alt="User 1"
								class="rounded-full"
							/>
						</Avatar>
						<Avatar class="h-14 w-14 border-2 border-purple-500/50">
							<img
								src="https://i.pinimg.com/474x/e4/f7/73/e4f77377b9c1a7cd8258210097d9f633.jpg?enhanced"
								alt="User 2"
								class="rounded-full"
							/>
						</Avatar>
						<Button
							variant="outline"
							class="h-14 w-14 rounded-full border-2 border-dashed border-gray-600 hover:border-purple-500 hover:bg-purple-500/10"
						>
							<span class="text-lg">+</span>
						</Button>
					</div>
					<div class="mb-8">
						<div class="mb-2 text-sm text-gray-400">Amount:</div>
						<div class="flex items-baseline gap-2">
							<span class="text-3xl font-semibold text-white">$3.25</span>
						</div>
					</div>
					<Button
						class="h-12 w-full rounded-xl bg-purple-600 font-medium text-white hover:bg-purple-700"
					>
						Transfer Now
					</Button>
				</Card>

				<!-- Market Trend -->
				<Card class="w-full rounded-2xl bg-[#1F1B2E]/80 p-6 backdrop-blur-sm lg:w-[400px]">
					<div class="mb-6 flex items-center justify-between">
						<h2 class="text-base font-medium text-white">Market Trend</h2>
						<div class="flex items-center gap-8 text-xs text-gray-400">
							<span>Last Price</span>
							<span>24h Change</span>
						</div>
					</div>
					<div class="space-y-5">
						{#each marketTrends as trend}
							<div class="flex items-center justify-between">
								<div class="flex flex-col">
									<div class="flex items-center gap-2">
										<span class="text-white">{trend.name}</span>
										<span class="hidden text-xs text-gray-400 md:block">{trend.fullName}</span>
									</div>
								</div>
								<div class="flex items-center gap-8">
									<span class="text-sm text-white">{trend.price}</span>
									<div class="flex min-w-[60px] items-center justify-end gap-1">
										<span
											class="text-sm {trend.trend === 'up' ? 'text-green-500' : 'text-red-500'}"
										>
											{trend.trend === 'up' ? '↑' : '↓'}
										</span>
										<span
											class="text-sm {trend.trend === 'up' ? 'text-green-500' : 'text-red-500'}"
										>
											{trend.change}%
										</span>
									</div>
								</div>
							</div>
						{/each}
					</div>
				</Card>
			</div>
		</main>
	</div>
</div>

<style>
	@keyframes float-1 {
		0%,
		140% {
			transform: translate(0, 0) rotate(45deg);
		}
		50% {
			transform: translate(-14px, -20px) rotate(45deg);
		}
	}

	@keyframes float-2 {
		0%,
		140% {
			transform: translate(0, 0) rotate(-12deg);
		}
		50% {
			transform: translate(15px, -15px) rotate(-12deg);
		}
	}

	@keyframes float-3 {
		0%,
		140% {
			transform: translate(0, 0) rotate(12deg);
		}
		50% {
			transform: translate(-20px, 14px) rotate(12deg);
		}
	}

	.animate-float-1 {
		animation: float-1 6s ease-in-out infinite;
	}
	.animate-float-2 {
		animation: float-2 7s ease-in-out infinite;
	}
	.animate-float-3 {
		animation: float-3 8s ease-in-out infinite;
	}
</style>
