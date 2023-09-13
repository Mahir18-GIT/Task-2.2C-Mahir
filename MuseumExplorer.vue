<template>
    <div :class="['container', theme]">
        <nav>
            <ul>
                <li><a href="#">Home</a></li>
                <li><a href="#">Explore</a></li>
                <li><a href="#">About</a></li>
                <li><a href="#">Contact</a></li>
                <li><button @click="toggleTheme">{{ theme === 'light' ? 'Dark Mode' : 'Light Mode' }}</button></li>
            </ul>
        </nav>

        <!-- Image Slider -->
        <div class="image-slider">
            <img :src="images[currentImageIndex]" alt="Museum Image" class="slider-image">
            <button class="slider-btn" @click="prevImage">←</button>
            <button class="slider-btn" @click="nextImage">→</button>
        </div>

        <section class="museum-section">
            <h2>Select a Museum</h2>
            <select v-model="selectedMuseum" class="museum-select">
                <option v-for="museum in museums" :value="museum.name" :key="museum.name">{{ museum.name }}</option>
            </select>
            <p v-if="selectedMuseum">Description: {{ museums.find(m => m.name === selectedMuseum).description }}</p>
        </section>

        <!-- Feedback Form -->
        <section class="feedback-section">
            <h2>Feedback</h2>
            <form @submit.prevent="submitFeedback">
                <div class="input-group">
                    <label for="name">Name:</label>
                    <input type="text" id="name" v-model="feedback.name" required>
                </div>
                <div class="input-group">
                    <label for="comments">Comments:</label>
                    <textarea id="comments" v-model="feedback.comments" required></textarea>
                </div>
                <button type="submit" class="submit-btn">Submit</button>
            </form>
        </section>

        <footer>
            <p>&copy; 2023 Virtual Museum Explorer. All rights reserved.</p>
        </footer>
    </div>
</template>

<script>
export default {
    data() {
        return {
            theme: 'light',
            museums: [
                {name: "Louvre", description: "Home to the Mona Lisa."},
                {name: "Metropolitan Museum of Art", description: "Located in New York City."},
                {name: "British Museum", description: "Located in London."}
            ],
            selectedMuseum: null,
            images: [
                "https://images.hindustantimes.com/img/2023/01/14/1600x900/louvre_museum_1647326845807_1673697548887_1673697548887.jpg",
                "https://lh3.googleusercontent.com/p/AF1QipOCqBHgVqIS-Mw4j1mS1U3rkKDQ9u5FqoZ_4I8=s1360-w1360-h1020",
                "https://lh3.googleusercontent.com/p/AF1QipPJA1W3rAPK3xAArAOtYdTMu5rgRDbkTAotGV3t=s1360-w1360-h1020"
            ],
            currentImageIndex: 0,
            feedback: {
                name: '',
                comments: ''
            }
        };
    },
    methods: {
        toggleTheme() {
            this.theme = this.theme === 'light' ? 'dark' : 'light';
        },
        nextImage() {
            if (this.currentImageIndex < this.images.length - 1) {
                this.currentImageIndex++;
            } else {
                this.currentImageIndex = 0;
            }
        },
        prevImage() {
            if (this.currentImageIndex > 0) {
                this.currentImageIndex--;
            } else {
                this.currentImageIndex = this.images.length - 1;
            }
        },
        submitFeedback() {
            console.log("Feedback submitted:", this.feedback);
            alert("Thanks for your feedback!");
            this.feedback.name = '';
            this.feedback.comments = '';
        }
    }
}
</script>

<style scoped>
body, html {
 height: 100%;
    margin: 0;
    padding: 0;
    font-family: 'Arial', sans-serif;
    background: linear-gradient(rgba(0, 0, 0, 0.4), rgba(0, 0, 0, 0.4)), url('https://source.unsplash.com/random/1920x1080?museum') no-repeat center center fixed;
    background-size: cover;
}

.container {
    max-width: 980px;
    margin: 20px auto;
    background-color: rgba(255, 255, 255, 0.95);
    padding: 20px 40px;
    border-radius: 15px;
    box-shadow: 0px 5px 30px rgba(0, 0, 0, 0.2);
    backdrop-filter: blur(10px);
}

nav ul {
    list-style-type: none;
    margin: 0;
    padding: 0;
    display: flex;
    justify-content: space-between;
    background-color: rgba(0, 0, 0, 0.7);
    border-radius: 5px;
    overflow: hidden;
}

nav li {
    flex-grow: 1;
    text-align: center;
}

nav a, nav button {
    display: block;
    padding: 10px 20px;
    text-decoration: none;
    color: white;
    transition: background 0.3s;
}

nav a:hover, nav button:hover {
    background-color: #555;
}

.image-slider {
    position: relative;
    margin: 30px 0;
}

.slider-image {
    max-width: 100%;
    display: block;
    margin: 0 auto;
    height: 400px;
    object-fit: cover;
    border-radius: 10px;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.15);
}

.image-slider button {
    background-color: rgba(0, 0, 0, 0.6);
    color: white;
    padding: 10px 20px;
    border: none;
    cursor: pointer;
    border-radius: 50%;
    font-size: 24px;
    transition: background 0.3s, transform 0.3s;
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
}

.image-slider button:hover {
    background-color: rgba(0, 0, 0, 0.8);
    transform: translateY(-50%) scale(1.1);
}

.image-slider .slider-btn:nth-child(2) {
    left: 5%;
}

.image-slider .slider-btn:nth-child(3) {
    right: 5%;
}

.museum-section h2, .feedback-section h2 {
    text-align: center;
    margin-bottom: 20px;
}

.museum-select {
    width: 100%;
    padding: 10px;
    border-radius: 5px;
    border: 1px solid #ccc;
    font-size: 16px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.input-group {
    margin-bottom: 20px;
}

.input-group label {
    display: block;
    margin-bottom: 8px;
}

.input-group textarea, .input-group input {
    width: 100%;
    padding: 10px;
    border-radius: 5px;
    border: 1px solid #ccc;
    font-size: 16px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.submit-btn {
    background-color: #333;
    color: white;
    padding: 10px 20px;
    border: none;
    cursor: pointer;
    border-radius: 5px;
    transition: background 0.3s;
}

.submit-btn:hover {
    background-color: #555;
}

footer {
    padding: 20px;
    background-color: rgba(0, 0, 0, 0.5);
    color: white;
    text-align: center;
    border-radius: 5px;
    margin-top: 30px;
}

/* Dark Theme */
.container.dark {
    background-color: rgba(10, 10, 10, 0.9);
}

.container.dark nav ul, .container.dark .submit-btn, .container.dark footer {
    background-color: rgba(34, 34, 34, 0.9);
}

.container.dark nav a, .container.dark nav button, .container.dark .submit-btn {
    color: #f4f4f4;
}

.container.dark nav a:hover, .container.dark nav button:hover, .container.dark .submit-btn:hover {
    background-color: #444;
}

@media screen and (max-width: 600px) {
    nav li {
        width: 100%;
        text-align: center;
    }
}
</style>