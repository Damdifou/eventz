<script>
	import '../app.postcss'
	import ThemeSelect from "$lib/theme-select.svelte";
</script>

<div class="w-full p-2xl">
	<main class="w-full flex flex-col h-screen content-center justify-center">
		<div class="bg-transparent w-full m-auto">
			<div class="bg-transparent rounded shadow px-4 pt-5 pb-4 sm:p-6 sm:pb-4">
				<slot />
			</div>
			<div class="fixed navbar top-0 left-auto right-0 bg-transparent/20 ">
				<div class="flex-1">
					<button class="btn btn-ghost text-xl">
						<a href="/">Coucou</a>
					</button>
				</div>
				<div class="flex justify-end flex-1 px-2">
					<div class="flex items-stretch">
						<button class="btn btn-ghost rounded-btn">
							<a href="/about">j'explore</a>
						</button>
						<div class="dropdown dropdown-end">
							<button tabindex="0" class="btn btn-ghost rounded-btn">
								<a href="/todo">Todo</a>
							</button>
						</div>
						<div class="dropdown dropdown-end">
							<button tabindex="0" class="btn btn-ghost rounded-btn">Categorie</button>
							<button tabindex="0" class="menu dropdown-content z-[1] p-2 shadow bg-base-100 rounded-box w-52 mt-4">
								<li><button>Item 1</button></li>
								<li><button>Item 2</button></li>
							</button>
						</div>
					</div>
				</div>
				<div class="flex-none gap-2">

					<ThemeSelect />

					<div class="dropdown dropdown-end">
						<button tabindex="0" class="btn btn-ghost btn-circle avatar">
							<div class="w-10 rounded-full">
								<img src="../1.jpg" alt="Profil" />
							</div>
						</button>
						<button class="mt-3 z-[1] p-2 shadow menu menu-sm dropdown-content bg-base-100 rounded-box w-52" tabindex="0">
							<button class="btn" onclick="my_modal_1.showModal()">Login</button>
							<dialog id="my_modal_1" class="modal">
								<form method="dialog" class="modal-box">
									<h3 class="font-bold text-lg">Hello!</h3>
									<div class="modal-action">
										<div class="form-control w-full max-w-xs">
											<input type="text" placeholder="Pseudo" class="input input-bordered w-full max-w-xs" />
											<input type="text" placeholder="MdP" class="input input-bordered w-full max-w-xs" />
										</div>
										<!-- if there is a button in form, it will close the modal -->
										<button class="btn">Close</button>
									</div>
								</form>
							</dialog>
							<li><button>Profile</button></li>
							<li><button>Settings</button></li>
							<li><button>Logout</button></li>
						</button>
					</div>
				</div>
			</div>
		</div>
	</main>
</div>