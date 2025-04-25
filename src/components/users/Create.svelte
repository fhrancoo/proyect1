<script lang="ts">


const handleSubmit = async (event) => {
  try {
  event.preventDefault();
  const formData = new FormData(event.target);
  const data = Object.fromEntries(formData);

  await fetch('http://127.0.0.1:3000/user', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify(data),
  }).then((response) => response.json())
  } catch (error) {
    console.error(error);
  } finally {
    event.target.reset();
  }
}
</script>

<div class="min-h-screen bg-gradient-to-br from-blue-500 to-purple-600 py-6 flex flex-col justify-center sm:py-12">
  <div class="relative py-3 sm:max-w-xl sm:mx-auto">
    <div class="absolute inset-0 bg-gradient-to-r from-blue-300 to-purple-300 shadow-lg transform -skew-y-6 sm:skew-y-0 sm:-rotate-6 sm:rounded-3xl"></div>
    <div class="relative px-4 py-10 bg-white shadow-lg sm:rounded-3xl sm:p-20">
      <div class="max-w-md mx-auto">
        <div class="divide-y divide-gray-200">
          <div class="py-8 text-base leading-6 space-y-4 text-gray-700 sm:text-lg sm:leading-7">
            <div class="text-2xl font-bold text-center mb-8 text-gray-800">Create Account</div>
            <form onsubmit={handleSubmit} class="space-y-8">
              <div class="relative">
                <input 
                  type="text" 
                  class="peer h-12 w-full border-2 border-gray-300 rounded-lg px-4 text-gray-900 placeholder-transparent focus:outline-none focus:border-purple-600 focus:ring-2 focus:ring-purple-200 transition-all duration-200" 
                  placeholder="Name"
                  name="name"
                />
                <label class="absolute left-2 -top-2.5 bg-white px-2 text-sm text-gray-600 transition-all peer-placeholder-shown:text-base peer-placeholder-shown:text-gray-400 peer-placeholder-shown:top-3.5 peer-focus:-top-2.5 peer-focus:text-purple-600 peer-focus:text-sm">
                  Name
                </label>
              </div>
              
              <div class="relative">
                <input 
                  type="email" 
                  class="peer h-12 w-full border-2 border-gray-300 rounded-lg px-4 text-gray-900 placeholder-transparent focus:outline-none focus:border-purple-600 focus:ring-2 focus:ring-purple-200 transition-all duration-200" 
                  placeholder="Email address"
                  name="email"
                />
                <label class="absolute left-2 -top-2.5 bg-white px-2 text-sm text-gray-600 transition-all peer-placeholder-shown:text-base peer-placeholder-shown:text-gray-400 peer-placeholder-shown:top-3.5 peer-focus:-top-2.5 peer-focus:text-purple-600 peer-focus:text-sm">
                  Email address
                </label>
              </div>

              <div class="relative pt-4">
                <button class="w-full bg-gradient-to-r from-blue-500 to-purple-600 text-white rounded-lg px-6 py-3 font-semibold text-lg shadow-lg hover:shadow-xl transform hover:-translate-y-0.5 transition-all duration-200 focus:outline-none focus:ring-2 focus:ring-purple-500 focus:ring-opacity-50">
                  Create Account
                </button>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
