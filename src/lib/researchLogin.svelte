<script>
    import toast, { Toaster } from "svelte-french-toast";
    import { serverUrl } from "./constants";
    import { orgInfo } from "./store";
    import { onMount } from "svelte";
    let id = "";
    let password = "";
    let isLoading = true;

    async function handleSubmit(event) {
        const form = event.target;
        const data = new FormData(form);

        await fetch(serverUrl + "research/login", {
            method: "POST",
            body: data,
        })
            .then((response) => {
                return response.json();
            })
            .catch(() => null)
            .then((data) => {
                // let ret = +data;
                console.log(data);

                //Login Failed
                if (!data) {
                    toast.error("Login Failed 🙁");
                }
                //Login Failed
                else {
                    orgInfo.set({ orgInfo: data });
                    window.location.hash = `#/researchOrg/home`;
                }
            });

        form.reset();
    }
    function navigateHome() {
        window.location.hash = `#/`;
    }
    onMount(() => {
        setTimeout(() => {
            isLoading = false;
        }, 1500); // Simulating an async load for the image.
    });
    //bg-gradient-to-r from-neutral-300 to-stone-400
</script>

<Toaster />
<main class="container">
    {#if isLoading}
        <div class="loader mr-2" />
        <div>
            <h1 class="text-3xl font-bold">Loading...</h1>
        </div>
    {:else}
        <img
            src="https://aaitclybvvendvuswytq.supabase.co/storage/v1/object/public/BDeHR/back-button-new.svg"
            alt="Notification Icon"
            class="absolute top-4 left-4 h-10 w-10 transition-transform transform hover:scale-125"
            on:click={navigateHome}
        />
        <section
            class="min-h-screen flex items-center justify-center py-12 px-4 sm:px-6 lg:px-8"
        >
            <div
                class="flex bg-white shadow-2xl rounded-xl overflow-hidden max-w-4xl"
            >
                <!-- Photo on the left side of the card -->
                <div
                    class="hidden md:flex md:w-2/5 lg:w-2/5 items-center justify-center p-6"
                >
                    <img
                        src="https://aaitclybvvendvuswytq.supabase.co/storage/v1/object/public/BDeHR/medical-research-concept-icon-arthritis-clinic-services-abstract-idea-thin-line-illustration-doctor-checkup-and-examination-diagnosis-isolated-outline-color-drawing-editable-stroke-vector.jpg"
                        alt="User"
                        class="max-w-full max-h-full object-contain"
                    />
                </div>

                <!-- Previous Card Content -->
                <div class="w-full md:w-3/5 lg:w-3/5 p-8">
                    <div>
                        <img
                            class="mx-auto h-16 w-auto mb-6"
                            src="https://aaitclybvvendvuswytq.supabase.co/storage/v1/object/public/BDeHR/mainlogoBag.png"
                            alt="Your Logo"
                        />
                        <div class="flex flex-col items-center space-x-2 mb-2">
                            <img
                                src="https://aaitclybvvendvuswytq.supabase.co/storage/v1/object/public/BDeHR/analysis-svgrepo-com.svg"
                                class="w-16 h-16 transform transition duration-300 hover:rotate-12 hover:scale-110"
                                alt="Email Icon"
                            />
                            <p class="text-3xl font-extrabold text-blue-800">
                                Research Center
                            </p>
                        </div>
                        <h2
                            class="mt-2 text-center text-3xl font-extrabold text-gray-900"
                        >
                            Sign in to your account
                        </h2>
                    </div>
                    <form
                        class="mt-8 space-y-6"
                        on:submit|preventDefault={handleSubmit}
                    >
                        <div class="rounded-md shadow-sm -space-y-px">
                            <div>
                                <label for="userID" class="sr-only"
                                    >User ID</label
                                >
                                <input
                                    required
                                    bind:value={id}
                                    type="text"
                                    name="id"
                                    placeholder="Enter ID"
                                    class="appearance-none rounded-none relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 rounded-t-md focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm"
                                />
                            </div>
                            <div>
                                <label for="password" class="sr-only"
                                    >Password</label
                                >
                                <input
                                    required
                                    bind:value={password}
                                    type="password"
                                    name="password"
                                    placeholder="Enter Password"
                                    class="appearance-none rounded-none relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 rounded-b-md focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm"
                                />
                            </div>
                        </div>

                        <div class="flex items-center justify-between">
                            <div class="flex items-center">
                                <input
                                    id="remember_me"
                                    name="remember_me"
                                    type="checkbox"
                                    class="h-4 w-4 text-indigo-600 focus:ring-indigo-500 border-gray-300 rounded"
                                />
                                <label
                                    for="remember_me"
                                    class="ml-2 block text-sm text-gray-900"
                                >
                                    Remember me
                                </label>
                            </div>
                            <div class="text-sm">
                                <a
                                    href="#/researchsignup"
                                    class="font-medium text-indigo-600 hover:text-indigo-500"
                                >
                                    Don't Have an Account? Sign Up Here
                                </a>
                            </div>
                        </div>

                        <div>
                            <button
                                type="submit"
                                class="group w-full flex justify-center py-2 px-4 border border-transparent text-sm font-medium rounded-md text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
                            >
                                Sign In
                            </button>
                        </div>
                    </form>
                </div>
            </div>
        </section>
    {/if}
</main>

<style>
    .container {
        min-height: 100vh;
        min-width: 100vw;
        display: flex;
        justify-content: center;
        align-items: center;
        background: linear-gradient(120deg, #edf4ec, #c0c2c1);
    }

    .loader {
        border: 8px solid rgba(255, 255, 255, 0.1);
        border-radius: 50%;
        border-top: 8px solid white;
        width: 60px;
        height: 60px;
        animation: spin 1s linear infinite;
    }
</style>
