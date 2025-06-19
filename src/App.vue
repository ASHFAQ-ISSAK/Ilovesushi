<template>
  <div id="app">
    <nav class="navbar">
      <div class="nav-content">
        <div class="logo">🍣 I Love Sushi</div>
        <ul class="nav-links">
          <li><a href="#home" class="nav-link active">Home</a></li>
          <li><a href="#sushi-menu" class="nav-link">Our Sushi</a></li>
          <li><a href="#nairobi-sushi" class="nav-link">Nairobi Sushi</a></li>
          <li><a href="#exhibition" class="nav-link">Exhibition</a></li>
        </ul>
      </div>
    </nav>

    <main class="main-content">
      <section class="hero-section" id="home"> <h1 class="hero-title">I Love Sushi</h1>
        <p class="hero-subtitle">Authentic Japanese Cuisine • Fresh Daily • Made with Love</p>
      </section>

      <section id="sushi-menu" class="sushi-menu-section"> <div class="category-filters">
          <button
            class="filter-btn"
            :class="{ active: activeCategory === 'all' }"
            @click="filterSushi('all')"
          >
            All Sushi
          </button>
          <button
            class="filter-btn"
            :class="{ active: activeCategory === 'nigiri' }"
            @click="filterSushi('nigiri')"
          >
            Nigiri
          </button>
          <button
            class="filter-btn"
            :class="{ active: activeCategory === 'sashimi' }"
            @click="filterSushi('sashimi')"
          >
            Sashimi
          </button>
          <button
            class="filter-btn"
            :class="{ active: activeCategory === 'rolls' }"
            @click="filterSushi('rolls')"
          >
            Rolls
          </button>
          <button
            class="filter-btn"
            :class="{ active: activeCategory === 'vegan' }"
            @click="filterSushi('vegan')"
          >
            Vegan
          </button>
          <button
            class="filter-btn"
            :class="{ active: activeCategory === 'cooked' }"
            @click="filterSushi('cooked')"
          >
            Cooked
          </button>
        </div>

        <div class="sushi-container" :class="{ loading: loading }" id="sushiContainer">
          <div
            v-for="sushi in filteredSushi"
            :key="sushi.id"
            class="sushi-card"
            :class="{ selected: selectedSushi && selectedSushi.id === sushi.id }"
            @click="showRecipePopup(sushi)"
          >
            <div class="category-badge">{{ sushi.categoryDisplay }}</div>
            <div class="sushi-stack">
              <div :class="['sashimi', sushi.colorClass]" :style="sushi.sashimiStyle"></div>
              <div class="rice-base"></div>
            </div>
            <div class="sushi-name">{{ sushi.name }}</div>
            <div class="sushi-description">{{ sushi.description }}</div>
            <div class="ingredients">
              <span v-for="ingredient in sushi.ingredients" :key="ingredient" class="ingredient-tag">
                {{ ingredient }}
              </span>
            </div>
            <button class="add-to-cart">View Recipe</button>
          </div>
        </div>
      </section>
    </main>

    <section id="nairobi-sushi" class="content-section light-background">
      <div class="content-wrapper">
        <h2 class="section-title">Sushi in Nairobi: Local Flavors & Sourcing</h2>
        <p class="section-subtitle">
          Discover how to enjoy sushi with fresh, local ingredients and where to find your sushi essentials right here in Nairobi.
        </p>

        <h3 class="subsection-title">Locally Inspired Sushi Rolls</h3>
        <p>Get creative with these sushi roll ideas that incorporate delicious and readily available Kenyan ingredients:</p>
        <ul class="info-list">
          <li>
            <strong>Tilapia Maki:</strong> Utilize fresh, pan-seared or grilled tilapia, flaked and mixed with a light sauce, perhaps with finely diced bell peppers or carrots for a local touch.
          </li>
          <li>
            <strong>Avocado & Mango Roll:</strong> Embrace Kenya's abundant avocados and ripe mangoes for a sweet, creamy, and vibrant vegetarian roll.
          </li>
          <li>
            <strong>Smoked Nile Perch Roll:</strong> Smoked Nile Perch offers a rich, savory flavor. Pair it with cucumber and optionally, a touch of cream cheese for a unique experience.
          </li>
          <li>
            <strong>Kachumbari Roll:</strong> A bold, vegetarian option inspired by the classic Kenyan Kachumbari (finely diced tomatoes, onions, and cilantro). Ensure ingredients are well-drained to maintain rice texture.
          </li>
          <li>
            <strong>Chicken Teriyaki Roll:</strong> A popular cooked sushi option worldwide. Use high-quality locally sourced chicken for a delicious, familiar flavor.
          </li>
          <li>
            <strong>Vegetable Medley Roll:</strong> Create colorful rolls with fresh Kenyan vegetables like carrots, cucumber, bell peppers, and finely blanched *sukuma wiki* for a healthy and accessible option.
          </li>
        </ul>

        <h3 class="subsection-title">Where to Buy Sushi Ingredients in Nairobi</h3>
        <p>Finding the right ingredients is key to making sushi at home. Here's a guide to sourcing your sushi essentials in Nairobi:</p>
        <ul class="info-list">
          <li>
            <strong>Sushi Rice & Nori (Seaweed Sheets):</strong>
            <ul>
              <li>
                <strong>Supermarkets:</strong> Large chains like Carrefour, Quickmart, and Chandarana Foodplus often have dedicated international food aisles where you can find Japanese short-grain rice and various brands of nori sheets.
              </li>
              <li>
                <strong>Specialty Stores:</strong> Keep an eye out for smaller Asian grocery stores, particularly in areas like Westlands or Kilimani, which may offer a wider selection.
              </li>
            </ul>
          </li>
          <li>
            <strong>Rice Vinegar, Soy Sauce, Wasabi & Pickled Ginger:</strong>
            <ul>
              <li>These essential condiments are widely available in the international food or condiments aisles of most major supermarkets across Nairobi.</li>
            </ul>
          </li>
          <li>
            <strong>Sushi-Grade Fish (for Raw Consumption):</strong>
            <p>Sourcing high-quality, safe fish for raw consumption requires careful attention to freshness and handling. Always inquire about its suitability for sushi.</p>
            <ul>
              <li>
                <strong>KAI Global LTD:</strong> Known for their sushi restaurants, KAI Global aims to supply high-quality fresh fish. It's worth contacting them directly to inquire about purchasing sushi-grade fish for home use. <br />
                Contact:
                <a href="tel:+254717112233" class="text-link">+254 717 11 22 33</a> or
                <a href="mailto:kyohei@kai.co.ke" class="text-link">kyohei@kai.co.ke</a> | Website:
                <a href="https://www.kai.co.ke/" target="_blank" rel="noopener noreferrer" class="text-link">www.kai.co.ke</a>
              </li>
              <li>
                <strong>Prime Cuts Butchery, Deli & Bistro:</strong> They offer fresh salmon fillet and yellowfin tuna loin steaks. While not explicitly labeled "sushi-grade," a reputable establishment like Prime Cuts maintains high standards. Always ask their staff about the specific fish's freshness and handling procedures if you intend to consume it raw. <br />
                Website:
                <a href="https://primecuts.co.ke/collections/fish-seafood" target="_blank" rel="noopener noreferrer" class="text-link">primecuts.co.ke/collections/fish-seafood</a>
              </li>
              <li>
                <strong>Trusted Fishmongers:</strong> Building a relationship with a reliable local fishmonger who can guarantee the freshness and origin of their seafood is invaluable. Look for fish with clear, bright eyes, firm flesh, and a fresh, mild sea smell.
              </li>
            </ul>
          </li>
          <li>
            <strong>Fresh Vegetables:</strong>
            <ul>
              <li>
                Nairobi's vibrant local markets (e.g., Marikiti, City Park Market) and all major supermarkets are excellent sources for fresh, crisp vegetables needed for your rolls.
              </li>
            </ul>
          </li>
        </ul>
        <p class="note-text text-center">
          <strong>Important Note on Fish Safety:</strong> When preparing sushi with raw fish at home, always prioritize freshness and proper handling to minimize health risks. If you are unsure about the quality, it's best to cook the fish thoroughly or opt for vegetarian/cooked sushi rolls.
        </p>
      </div>
    </section>

    <section id="exhibition" class="content-section">
      <div class="content-wrapper">
        <h2 class="section-title">The 'I Love Sushi' Exhibition: Nairobi 2025</h2>
        <p class="section-subtitle">
          Get ready to delve into the fascinating world of sushi! The "I Love Sushi" exhibition is a traveling cultural exhibition organized by The Japan Foundation.
        </p>

        <div class="exhibition-details-grid">
          <div class="exhibition-image-container">
            <img
              src="https://www.jpf.go.jp/assets/i-like-sushi.png"
              alt="I Love Sushi Exhibition Banner"
              class="exhibition-image"
            />
          </div>
          <div class="exhibition-text-content">
            <h3 class="subsection-title">About the Exhibition</h3>
            <p>
              This unique exhibition explores the history, culture, and artistry behind sushi, one of Japan's most iconic culinary traditions. It aims to deepen understanding and appreciation of Japanese food culture worldwide.
            </p>
            <p>
              The "I Love Sushi" exhibition is
              <strong class="highlight-text">scheduled for Kenya in the first semester of 2025</strong>. It is open all through june till july.
            </p>

            <h4 class="link-heading">Find Out More:</h4>
            <p class="link-description">
              For detailed information about the exhibition, including its global tour schedule and content, please visit The Japan Foundation's official page:
            </p>
            <a
              href="https://www.jpf.go.jp/e/project/culture/exhibit/traveling/sushi.html"
              target="_blank"
              rel="noopener noreferrer"
              class="action-button primary-button"
              >Visit The Japan Foundation (Global)</a
            >

            <p class="link-description mt-3">
              For confirmed dates, venue, and any local events related to the exhibition in Nairobi, keep an eye on the Embassy of Japan in Kenya's official website:
            </p>
            <a
              href="https://www.ke.emb-japan.go.jp/itpr_en/index.html"
              target="_blank"
              rel="noopener noreferrer"
              class="action-button secondary-button"
              >Embassy of Japan in Kenya</a
            >
          </div>
        </div>
      </div>
    </section>

    <div v-if="selectedSushi" class="modal-overlay" @click.self="closeRecipePopup">
      <div class="modal-content">
        <button class="close-modal" @click="closeRecipePopup">&times;</button>
        <h2>{{ selectedSushi.name }}</h2>
        <p class="modal-description">{{ selectedSushi.description }}</p>
        <div class="modal-recipe-details">
          <h3>Ingredients:</h3>
          <ul class="modal-ingredients-list">
            <li v-for="ingredient in selectedSushi.ingredients" :key="ingredient">
              {{ ingredient }}
            </li>
          </ul>
          <h3>Instructions:</h3>
          <ol class="modal-instructions-list">
            <li v-for="(step, index) in selectedSushi.detailedSteps" :key="index">
              {{ step }}
            </li>
          </ol>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';

// Reactive state for sushi data and filtering
const sushiData = ref([
  {
    id: 1,
    name: 'Tuna Nigiri',
    description: 'Classic tuna nigiri with fresh, high-quality tuna.',
    category: 'nigiri',
    categoryDisplay: 'Nigiri',
    colorClass: 'tuna',
    sashimiStyle: { backgroundColor: '#FF6347' },
    ingredients: ['Sushi Rice', 'Tuna (Maguro)', 'Nori (small strip)', 'Wasabi', 'Soy Sauce'],
    detailedSteps: [
      'Prepare sushi rice according to package instructions, ensuring it’s seasoned with sushi vinegar.',
      'Slice fresh, sushi-grade tuna into thin, uniform pieces, about 2 inches long and 1 inch wide.',
      'Moisten your hands with water (tezu) to prevent sticking. Form a small, oval-shaped mound of sushi rice, about 1.5 inches long.',
      'Dab a tiny bit of wasabi onto the rice.',
      'Place a tuna slice on top of the rice, gently pressing and molding it to fit the rice perfectly.',
      'Serve immediately with soy sauce and extra wasabi on the side.'
    ]
  },
  {
    id: 2,
    name: 'Salmon Nigiri',
    description: 'Delicate salmon nigiri, a favorite for its rich flavor.',
    category: 'nigiri',
    categoryDisplay: 'Nigiri',
    colorClass: 'salmon',
    sashimiStyle: { backgroundColor: '#FFA07A' },
    ingredients: ['Sushi Rice', 'Salmon (Sake)', 'Wasabi', 'Soy Sauce'],
    detailedSteps: [
      'Prepare seasoned sushi rice as described for Tuna Nigiri.',
      'Slice fresh, sushi-grade salmon thinly against the grain into pieces similar in size to the tuna slices.',
      'With wet hands, form oval shapes from the sushi rice.',
      'Apply a small dab of wasabi to the rice.',
      'Gently place the salmon slice over the rice, molding it with your fingers to create a neat nigiri piece.',
      'Serve fresh with soy sauce.'
    ]
  },
  {
    id: 3,
    name: 'California Roll',
    description: 'A popular Western-style roll with avocado, cucumber, and crab meat.',
    category: 'rolls',
    categoryDisplay: 'Rolls',
    colorClass: 'california',
    sashimiStyle: { backgroundColor: '#F0E68C' },
    ingredients: ['Sushi Rice', 'Nori', 'Avocado', 'Cucumber', 'Crab Stick', 'Sesame Seeds', 'Mayonnaise'],
    detailedSteps: [
      'Lay a sheet of nori on a bamboo rolling mat (makisu). Spread a thin, even layer of seasoned sushi rice over the nori, leaving a small border at the top.',
      'Sprinkle sesame seeds over the rice if desired. Carefully flip the nori sheet over so the rice is now facing down.',
      'Place strips of avocado, cucumber, and crab stick (or imitation crab) horizontally across the center of the nori.',
      'Starting from the end closest to you, tightly roll the mat, pressing gently to form a compact roll.',
      'Using a very sharp, wet knife, slice the roll into 8 equal pieces.',
      'Serve with a side of mayonnaise or spicy mayo if preferred.'
    ]
  },
  {
    id: 4,
    name: 'Avocado Roll',
    description: 'Simple and creamy, a classic vegan sushi roll.',
    category: 'vegan',
    categoryDisplay: 'Vegan',
    colorClass: 'avocado',
    sashimiStyle: { backgroundColor: '#9ACD32' },
    ingredients: ['Sushi Rice', 'Nori', 'Avocado', 'Sesame Seeds'],
    detailedSteps: [
      'Place a half sheet of nori on a bamboo mat. Spread seasoned sushi rice evenly over the nori, leaving about a 1/2 inch border at the top.',
      'Arrange thin slices of ripe avocado horizontally across the lower third of the rice.',
      'Carefully roll the mat from the bottom, pressing firmly to create a tight cylinder.',
      'Moisten your knife and slice the roll into 6-8 pieces. Optionally, sprinkle with sesame seeds.',
      'Serve immediately.'
    ]
  },
  {
    id: 5,
    name: 'Shrimp Tempura Roll',
    description: 'Crispy fried shrimp tempura in a delicious roll.',
    category: 'cooked',
    categoryDisplay: 'Cooked',
    colorClass: 'shrimp',
    sashimiStyle: { backgroundColor: '#FF8C00' },
    ingredients: ['Sushi Rice', 'Nori', 'Shrimp Tempura', 'Avocado', 'Cucumber', 'Spicy Mayo'],
    detailedSteps: [
      'Prepare shrimp tempura (can be store-bought frozen and fried, or homemade). Ensure it is crispy and cooled slightly.',
      'Lay a sheet of nori on a bamboo mat. Spread seasoned sushi rice evenly, leaving a small border.',
      'Place one or two pieces of shrimp tempura along the center, adding thin slices of avocado and cucumber next to them.',
      'Drizzle with spicy mayonnaise if desired.',
      'Roll tightly, applying gentle pressure as you go, and slice into 8-10 pieces using a wet, sharp knife.',
      'Serve warm or at room temperature.'
    ]
  },
  {
    id: 6,
    name: 'Tuna Sashimi',
    description: 'Thick slices of fresh tuna, served without rice.',
    category: 'sashimi',
    categoryDisplay: 'Sashimi',
    colorClass: 'tuna-sashimi',
    sashimiStyle: { backgroundColor: '#FF6347' },
    ingredients: ['Tuna (Maguro)', 'Daikon Radish', 'Shiso Leaf', 'Soy Sauce', 'Wasabi'],
    detailedSteps: [
      'Obtain the freshest, sushi-grade tuna. This is crucial for raw consumption.',
      'Using a very sharp knife, slice the tuna against the grain into thick, uniform pieces, about 1/2 inch thick.',
      'Arrange the sashimi artfully on a chilled platter, often garnished with finely shredded daikon radish and shiso leaves.',
      'Serve immediately with small dishes of soy sauce and a dollop of wasabi for dipping.'
    ]
  },
  {
    id: 7,
    name: 'Cucumber Roll',
    description: 'Light and crisp vegetarian roll.',
    category: 'vegan',
    categoryDisplay: 'Vegan',
    colorClass: 'green',
    sashimiStyle: { backgroundColor: '#A2D149' },
    ingredients: ['Cucumber', 'Nori', 'Sushi Rice'],
    detailedSteps: [
      'Peel and julienne a cucumber into thin, matchstick-sized strips. Remove any watery seeds from the center.',
      'Lay a half sheet of nori on a bamboo mat. Spread seasoned sushi rice thinly over the nori.',
      'Place a line of cucumber strips across the center of the rice.',
      'Roll tightly, moisten the edge of the nori to seal, and slice into 6-8 pieces with a wet knife.',
      'Serve as a refreshing, simple sushi.'
    ]
  },
  {
    id: 8,
    name: 'Spicy Tuna Roll',
    description: 'Tuna with a spicy kick.',
    category: 'rolls',
    categoryDisplay: 'Rolls',
    colorClass: 'red',
    sashimiStyle: { backgroundColor: '#E74C3C' },
    ingredients: ['Tuna', 'Sriracha', 'Mayonnaise', 'Nori', 'Sushi Rice', 'Green Onion (optional)'],
    detailedSteps: [
      'Finely dice sushi-grade tuna. In a bowl, mix the diced tuna with sriracha and mayonnaise to your desired level of spice.',
      'Lay a sheet of nori on a bamboo mat. Spread a thin layer of seasoned sushi rice over the nori, leaving a small border.',
      'If making an inside-out roll, sprinkle with sesame seeds and flip. Place the spicy tuna mixture along the center of the nori. Add finely chopped green onion if using.',
      'Roll tightly and carefully slice into 8 pieces with a wet, sharp knife.',
      'Serve immediately for the best flavor.'
    ]
  },
  {
    id: 9,
    name: 'Egg (Tamago) Nigiri',
    description: 'Sweet omelette over rice.',
    category: 'cooked',
    categoryDisplay: 'Cooked',
    colorClass: 'yellow',
    sashimiStyle: { backgroundColor: '#FCE883' },
    ingredients: ['Eggs', 'Sugar', 'Soy Sauce', 'Mirin', 'Dashi (optional)', 'Sushi Rice', 'Nori (strip)'],
    detailedSteps: [
      'Prepare Tamagoyaki: Whisk eggs with sugar, soy sauce, mirin, and dashi (if using). Cook in layers in a rectangular tamagoyaki pan until a thick, sweet omelette is formed. Let it cool.',
      'Slice the cooled tamagoyaki into rectangular pieces, roughly the size of a nigiri topping.',
      'Form small oval mounds of seasoned sushi rice with wet hands.',
      'Place a slice of tamagoyaki on top of each rice mound. Optionally, wrap a thin strip of nori around the middle to secure it.',
      'Serve as a delightful, mildly sweet sushi piece.'
    ]
  },
  {
    id: 10,
    name: 'Vegetable Futomaki',
    description: 'Thick roll with mixed vegetables.',
    category: 'vegan',
    categoryDisplay: 'Vegan',
    colorClass: 'veggie',
    sashimiStyle: { backgroundColor: '#7CB342' },
    ingredients: ['Sushi Rice', 'Whole Nori Sheet', 'Carrot', 'Cucumber', 'Avocado', 'Cooked Spinach', 'Kanpyo (optional)'],
    detailedSteps: [
      'Prepare various vegetables by cutting them into long, thin strips (e.g., blanched carrot, julienned cucumber, avocado slices, cooked and squeezed spinach). If using kanpyo, rehydrate and simmer it in a dashi-soy-sugar broth.',
      'Lay a full sheet of nori on a bamboo mat. Spread a generous, even layer of seasoned sushi rice over the entire nori.',
      'Arrange the prepared vegetable strips in a neat line across the center of the rice, making sure to include a variety of colors and textures.',
      'Carefully roll the bamboo mat tightly from the bottom, pressing firmly to create a large, compact roll.',
      'Using a very sharp, wet knife, slice the thick futomaki roll into 6-8 large, beautiful pieces.',
      'Serve as a hearty and colorful vegetarian sushi option.'
    ]
  },
  {
    id: 11,
    name: 'Crab Stick Nigiri',
    description: 'Simple crab over vinegared rice.',
    category: 'cooked',
    categoryDisplay: 'Cooked',
    colorClass: 'crab',
    sashimiStyle: { backgroundColor: '#FF9999' },
    ingredients: ['Crab Stick (Surimi)', 'Sushi Rice', 'Nori (small strip)', 'Wasabi (optional)'],
    detailedSteps: [
      'Prepare seasoned sushi rice.',
      'Take a crab stick and gently unroll or flatten it slightly if necessary to create a wider surface.',
      'With wet hands, form small oval shapes of sushi rice.',
      'Optionally, dab a tiny bit of wasabi on the rice.',
      'Place the crab stick on top of the rice, molding it slightly. Secure it with a thin strip of nori wrapped around the middle if desired.',
      'Serve as a quick and popular cooked sushi item.'
    ]
  },
  {
    id: 12,
    name: 'Teriyaki Chicken Roll',
    description: 'Cooked chicken with teriyaki sauce.',
    category: 'cooked',
    categoryDisplay: 'Cooked',
    colorClass: 'brown',
    sashimiStyle: { backgroundColor: '#A0522D' },
    ingredients: ['Chicken Breast', 'Teriyaki Sauce', 'Sushi Rice', 'Nori', 'Cucumber (strips)', 'Sesame Seeds'],
    detailedSteps: [
      'Cook chicken breast until thoroughly done. Shred or slice it into thin pieces. Toss the cooked chicken with your favorite teriyaki sauce until well coated.',
      'Lay a sheet of nori on a bamboo mat. Spread seasoned sushi rice evenly over the nori, leaving a small border.',
      'Place a line of teriyaki chicken and cucumber strips across the center of the rice.',
      'Roll tightly, moisten the edge of the nori to seal, and slice into 8 pieces with a wet, sharp knife.',
      'Optionally, drizzle with extra teriyaki sauce and sprinkle with sesame seeds before serving.'
    ]
  },
  {
    id: 13,
    name: 'Inari Sushi',
    description: 'Sweet tofu pouches stuffed with rice.',
    category: 'vegan',
    categoryDisplay: 'Vegan',
    colorClass: 'tofu',
    sashimiStyle: { backgroundColor: '#FFD700' },
    ingredients: ['Inari Age (seasoned fried tofu pouches)', 'Sushi Rice', 'Sesame Seeds (optional)'],
    detailedSteps: [
      'Gently open the pre-seasoned Inari Age (tofu pouches). They are usually sold in airtight packages and are ready to use.',
      'Prepare seasoned sushi rice. Allow it to cool slightly so it\'s easier to handle.',
      'Loosely fill each tofu pouch with the seasoned sushi rice. Do not pack it too tightly, as this can make the rice hard.',
      'Optionally, sprinkle the top of the rice with sesame seeds for added flavor and texture.',
      'Serve chilled or at room temperature as a popular sweet and savory vegan sushi.'
    ]
  },
  {
    id: 14,
    name: 'Kani Salad Gunkan',
    description: 'Crab mayo salad wrapped in nori.',
    category: 'rolls',
    categoryDisplay: 'Rolls',
    colorClass: 'creamy',
    sashimiStyle: { backgroundColor: '#FFE4B5' },
    ingredients: ['Crab Stick (Surimi)', 'Mayonnaise', 'Sriracha (optional)', 'Cucumber (diced)', 'Sushi Rice', 'Nori (strips)'],
    detailedSteps: [
      'Shred or finely dice crab sticks. In a bowl, mix the crab with mayonnaise and a dash of sriracha for a spicy kick (optional). Add finely diced cucumber for crunch.',
      'Form small, oval-shaped balls of seasoned sushi rice.',
      'Wrap a strip of nori tightly around the sides of each rice ball, allowing the nori to extend slightly above the rice to form a cup.',
      'Spoon a generous amount of the kani salad mixture on top of the rice within the nori cup.',
      'Serve immediately, possibly garnished with a touch of tobiko or more sriracha.'
    ]
  },
  {
    id: 15,
    name: 'Pickled Radish Roll',
    description: 'Sour-sweet daikon in a vegan roll.',
    category: 'vegan',
    categoryDisplay: 'Vegan',
    colorClass: 'radish',
    sashimiStyle: { backgroundColor: '#F4C430' },
    ingredients: ['Takuan (pickled daikon radish)', 'Sushi Rice', 'Nori'],
    detailedSteps: [
      'Obtain Takuan (yellow pickled daikon radish), often found in Asian grocery stores. Slice it into long, thin strips.',
      'Lay a half sheet of nori on a bamboo mat. Spread seasoned sushi rice thinly over the nori.',
      'Place one or two strips of Takuan horizontally across the center of the rice.',
      'Roll tightly using the bamboo mat, moisten the edge of the nori to seal, and slice into 6-8 pieces with a wet knife.',
      'Enjoy the unique sweet and tangy crunch of this traditional vegan roll.'
    ]
  },
  {
    id: 16,
    name: 'Mango Avocado Roll',
    description: 'Fruity and creamy vegan delight.',
    category: 'vegan',
    categoryDisplay: 'Vegan',
    colorClass: 'mango',
    sashimiStyle: { backgroundColor: '#FFD54F' },
    ingredients: ['Mango', 'Avocado', 'Sushi Rice', 'Nori', 'Sesame Seeds (optional)'],
    detailedSteps: [
      'Slice ripe mango and avocado into thin strips, ensuring they are not too soft.',
      'Lay a sheet of nori on a bamboo mat. Spread seasoned sushi rice thinly over the nori. If desired, sprinkle with sesame seeds and flip the nori so rice is facing down.',
      'Arrange mango and avocado strips across the center of the nori.',
      'Roll tightly, pressing gently to form a compact roll. Moisten the nori edge to seal.',
      'Using a very sharp, wet knife, slice the roll into 8 equal pieces.',
      'Serve as a sweet, refreshing, and colorful vegan sushi.'
    ]
  },
  {
    id: 17,
    name: 'Beef Teriyaki Roll',
    description: 'Grilled beef with sweet teriyaki sauce.',
    category: 'cooked',
    categoryDisplay: 'Cooked',
    colorClass: 'beef',
    sashimiStyle: { backgroundColor: '#8B4513' },
    ingredients: ['Thinly Sliced Beef', 'Teriyaki Sauce', 'Sushi Rice', 'Nori', 'Cucumber (strips)', 'Sesame Seeds'],
    detailedSteps: [
      'Thinly slice beef (e.g., sirloin or flank steak) and cook it, preferably grilled or pan-fried, then toss generously with teriyaki sauce until well coated and slightly caramelized.',
      'Lay a sheet of nori on a bamboo mat. Spread seasoned sushi rice over the nori, leaving a small border.',
      'Place a line of cooked teriyaki beef and thin cucumber strips across the center of the rice.',
      'Roll tightly and slice into 8 pieces with a wet, sharp knife.',
      'Garnish with extra teriyaki sauce and sesame seeds if desired.'
    ]
  },
  {
    id: 18,
    name: 'Eggplant Sushi',
    description: 'Grilled eggplant with soy glaze.',
    category: 'vegan',
    categoryDisplay: 'Vegan',
    colorClass: 'eggplant',
    sashimiStyle: { backgroundColor: '#9B59B6' },
    ingredients: ['Eggplant', 'Soy Sauce', 'Mirin', 'Sugar', 'Sushi Rice', 'Nori (small strip)'],
    detailedSteps: [
      'Slice eggplant into thin, bite-sized pieces. Lightly salt and let sit for 10 minutes, then pat dry.',
      'Grill or pan-fry the eggplant slices until tender. In a separate pan, simmer soy sauce, mirin, and a touch of sugar to create a savory glaze. Brush the cooked eggplant with this glaze.',
      'Form small oval mounds of seasoned sushi rice.',
      'Place a glazed eggplant slice on top of each rice mound. Optionally, secure with a thin strip of nori.',
      'Serve warm or at room temperature as a delicious vegan alternative.'
    ]
  },
  {
    id: 19,
    name: 'Sweet Corn Gunkan',
    description: 'Corn and mayo combo in nori wrap.',
    category: 'cooked',
    categoryDisplay: 'Cooked',
    colorClass: 'corn',
    sashimiStyle: { backgroundColor: '#FFF176' },
    ingredients: ['Canned Sweet Corn', 'Mayonnaise', 'Sushi Rice', 'Nori (strips)', 'Aonori (dried seaweed flakes, optional)'],
    detailedSteps: [
      'Drain canned sweet corn very well. In a small bowl, mix the drained corn with mayonnaise. Add a pinch of salt if needed.',
      'Form small, compact oval balls of seasoned sushi rice.',
      'Wrap a strip of nori tightly around the sides of each rice ball, letting the nori extend slightly above the rice to form a "cup."',
      'Spoon a generous amount of the sweet corn and mayonnaise mixture onto the top of the rice within the nori cup.',
      'Optionally, sprinkle with aonori (dried seaweed flakes) for extra flavor and visual appeal.',
      'Serve immediately.'
    ]
  },
  {
    id: 20,
    name: 'Sardine Roll',
    description: 'Kenyan-style roll with sardines.',
    category: 'cooked',
    categoryDisplay: 'Cooked',
    colorClass: 'silver',
    sashimiStyle: { backgroundColor: '#C0C0C0' },
    ingredients: ['Canned Sardines (in oil/water)', 'Avocado', 'Red Onion (finely diced)', 'Chili Flakes (optional)', 'Sushi Rice', 'Nori'],
    detailedSteps: [
      'Drain canned sardines well and flake them gently with a fork. Remove any large bones if desired.',
      'In a bowl, gently mix the flaked sardines with thinly sliced or diced avocado and a small amount of finely diced red onion. Add chili flakes if you like a bit of heat.',
      'Lay a sheet of nori on a bamboo mat. Spread seasoned sushi rice evenly over the nori.',
      'Place the sardine-avocado mixture along the center of the rice.',
      'Roll tightly and slice into 8 pieces with a wet, sharp knife.',
      'This roll offers a unique, savory flavor with a local twist.'
    ]
  },
  {
    id: 21,
    name: 'Tofu Avocado Roll',
    description: 'High-protein vegan sushi.',
    category: 'vegan',
    categoryDisplay: 'Vegan',
    colorClass: 'tofu',
    sashimiStyle: { backgroundColor: '#FFE0B2' },
    ingredients: ['Firm Tofu', 'Avocado', 'Soy Sauce', 'Sushi Rice', 'Nori', 'Sesame Seeds (optional)'],
    detailedSteps: [
      'Press firm tofu to remove excess water, then slice into thin strips. Lightly pan-fry or bake the tofu strips until golden brown and slightly firm. You can marinate them in a little soy sauce first.',
      'Slice ripe avocado into thin strips.',
      'Lay a sheet of nori on a bamboo mat. Spread seasoned sushi rice over the nori.',
      'Arrange the cooked tofu strips and avocado slices along the center of the rice.',
      'Roll tightly, pressing firmly to create a compact roll. Moisten the nori edge to seal.',
      'Slice into 8 pieces with a wet, sharp knife. Optionally, sprinkle with sesame seeds.',
      'Serve as a satisfying and healthy vegan sushi option.'
    ]
  },
  {
    id: 22,
    name: 'Kimchi Roll',
    description: 'Spicy Korean-style fermented roll.',
    category: 'vegan',
    categoryDisplay: 'Vegan',
    colorClass: 'kimchi',
    sashimiStyle: { backgroundColor: '#FF7043' },
    ingredients: ['Kimchi', 'Cucumber (strips)', 'Sesame Oil (optional)', 'Sushi Rice', 'Nori'],
    detailedSteps: [
      'Roughly chop kimchi and squeeze out any excess liquid to prevent the roll from becoming soggy. You can lightly sauté it with a touch of sesame oil for more flavor (optional).',
      'Lay a sheet of nori on a bamboo mat. Spread seasoned sushi rice evenly over the nori.',
      'Place a line of the prepared kimchi and thin cucumber strips across the center of the rice.',
      'Roll tightly and slice into 8 pieces with a wet, sharp knife.',
      'Serve this roll for a delicious spicy and tangy kick.'
    ]
  },
  {
    id: 23,
    name: 'Carrot Roll',
    description: 'Sweet, crunchy and easy to make.',
    category: 'vegan',
    categoryDisplay: 'Vegan',
    colorClass: 'orange',
    sashimiStyle: { backgroundColor: '#FFA726' },
    ingredients: ['Carrot', 'Sushi Rice', 'Nori', 'Sesame Seeds (optional)'],
    detailedSteps: [
      'Peel carrots and julienne them into thin, matchstick-sized strips. You can lightly blanch them in boiling water for 1-2 minutes to soften slightly and enhance sweetness, then cool rapidly in ice water and drain well.',
      'Lay a half sheet of nori on a bamboo mat. Spread seasoned sushi rice thinly over the nori.',
      'Place a line of carrot strips across the center of the rice.',
      'Roll tightly, moisten the edge of the nori to seal, and slice into 6-8 bite-sized pieces.',
      'Serve as a simple, crunchy, and naturally sweet vegan sushi option.'
    ]
  },
  {
    id: 24,
    name: 'Spicy Egg Gunkan',
    description: 'Boiled eggs with chili mayo.',
    category: 'cooked',
    categoryDisplay: 'Cooked',
    colorClass: 'spicy-egg',
    sashimiStyle: { backgroundColor: '#FFB74D' },
    ingredients: ['Hard-Boiled Eggs', 'Mayonnaise', 'Sriracha or Chili Sauce', 'Sushi Rice', 'Nori (strips)', 'Green Onion (garnish, optional)'],
    detailedSteps: [
      'Hard-boil eggs, peel, and then finely mash them in a bowl. Mix the mashed egg with mayonnaise and sriracha (or your preferred chili sauce) until well combined and creamy. Season with salt and pepper to taste.',
      'Form small, compact oval balls of seasoned sushi rice.',
      'Wrap a strip of nori tightly around the sides of each rice ball, letting the nori extend slightly above the rice to form a "cup."',
      'Spoon a generous amount of the spicy egg mixture onto the top of the rice within the nori cup.',
      'Garnish with finely chopped green onion if desired. Serve immediately.'
    ]
  },
  {
    id: 25,
    name: 'Kampyo Roll',
    description: 'Dried gourd roll, traditional and sweet.',
    category: 'vegan',
    categoryDisplay: 'Vegan',
    colorClass: 'kampyo',
    sashimiStyle: { backgroundColor: '#D4A373' },
    ingredients: ['Dried Kanpyo (gourd strips)', 'Soy Sauce', 'Mirin', 'Sugar', 'Dashi (optional)', 'Sushi Rice', 'Nori'],
    detailedSteps: [
      'Rehydrate dried kanpyo strips by soaking them in water for at least 30 minutes until soft. Rinse thoroughly, then simmer them in a mixture of soy sauce, mirin, sugar, and dashi (if using) until tender and flavorful, usually about 15-20 minutes. Drain and cool.',
      'Lay a half sheet of nori on a bamboo mat. Spread seasoned sushi rice thinly over the nori.',
      'Place a few strips of the cooked kanpyo across the center of the rice.',
      'Roll tightly, moisten the nori edge to seal, and slice into 6-8 pieces with a wet knife.',
      'Serve this traditional sweet and savory vegan roll.'
    ]
  },
  {
    id: 26,
    name: 'Boiled Egg Nigiri',
    description: 'Simple and filling.',
    category: 'cooked',
    categoryDisplay: 'Cooked',
    colorClass: 'boiled-egg',
    sashimiStyle: { backgroundColor: '#FFF9C4' },
    ingredients: ['Hard-Boiled Egg', 'Sushi Rice', 'Nori (small strip)', 'Soy Sauce (optional)'],
    detailedSteps: [
      'Hard-boil an egg, peel it, and slice it lengthwise or in thick, oval-shaped pieces.',
      'Form small, oval mounds of seasoned sushi rice with wet hands.',
      'Place a slice of hard-boiled egg on top of each rice mound. Secure it with a thin strip of nori wrapped around the middle.',
      'Serve as a simple, protein-rich, and cooked nigiri option, optionally with a dab of soy sauce.'
    ]
  },
  {
    id: 27,
    name: 'Cream Cheese Roll',
    description: 'Smooth and rich roll.',
    category: 'cooked',
    categoryDisplay: 'Cooked',
    colorClass: 'cream',
    sashimiStyle: { backgroundColor: '#FFFDE7' },
    ingredients: ['Cream Cheese', 'Cucumber (strips)', 'Sushi Rice', 'Nori', 'Sesame Seeds (optional)'],
    detailedSteps: [
      'Slice cream cheese into thin, rectangular sticks. Julienne cucumber into similar-sized strips.',
      'Lay a sheet of nori on a bamboo mat. Spread seasoned sushi rice evenly over the nori, leaving a small border.',
      'Place lines of cream cheese sticks and cucumber strips across the center of the rice.',
      'Roll tightly and slice into 8 pieces with a very sharp, wet knife to prevent sticking.',
      'Optionally, sprinkle with sesame seeds. This rich and creamy roll is a popular choice for those who prefer cooked ingredients.'
    ]
  },
  {
    id: 28,
    name: 'Mushroom Roll',
    description: 'Savory mushroom vegan roll.',
    category: 'vegan',
    categoryDisplay: 'Vegan',
    colorClass: 'mushroom',
    sashimiStyle: { backgroundColor: '#A1887F' },
    ingredients: ['Shiitake or Button Mushrooms', 'Soy Sauce', 'Mirin', 'Sushi Rice', 'Nori', 'Sesame Seeds (optional)'],
    detailedSteps: [
      'Clean and slice mushrooms (shiitake or button mushrooms work well). Sauté them in a pan with a little oil until tender. Add a splash of soy sauce and mirin to glaze and enhance their savory flavor. Let them cool.',
      'Lay a half sheet of nori on a bamboo mat. Spread seasoned sushi rice thinly over the nori.',
      'Place the cooled, sautéed mushroom slices along the center of the rice.',
      'Roll tightly, moisten the nori edge to seal, and slice into 6-8 pieces with a wet knife.',
      'Serve as an umami-rich and satisfying vegan sushi option.'
    ]
  },
  {
    id: 29,
    name: 'Banana Roll',
    description: 'Funky dessert-style vegan roll.',
    category: 'vegan',
    categoryDisplay: 'Vegan',
    colorClass: 'banana',
    sashimiStyle: { backgroundColor: '#FFF176' },
    ingredients: ['Ripe Banana', 'Peanut Butter (optional)', 'Chocolate Syrup (optional)', 'Sushi Rice', 'Nori'],
    detailedSteps: [
      'Peel and slice a ripe banana lengthwise into thin strips. If using peanut butter, spread a thin layer on the banana strips.',
      'Lay a half sheet of nori on a bamboo mat. Spread a thin layer of seasoned sushi rice over the nori.',
      'Place the banana (and peanut butter) strips across the center of the rice.',
      'Roll tightly, moisten the nori edge to seal, and slice into 6-8 pieces with a wet knife.',
      'Serve immediately as a unique dessert sushi, optionally drizzled with chocolate syrup or honey.'
    ]
  },
  {
    id: 30,
    name: 'Avocado Mango Gunkan',
    description: 'Bright, fruity gunkan-style sushi.',
    category: 'vegan',
    categoryDisplay: 'Vegan',
    colorClass: 'fruit',
    sashimiStyle: { backgroundColor: '#FDD835' },
    ingredients: ['Ripe Avocado (diced)', 'Ripe Mango (diced)', 'Lime Juice (optional)', 'Sushi Rice', 'Nori (strips)'],
    detailedSteps: [
      'Finely dice ripe avocado and mango. Gently mix them together. A squeeze of lime juice can prevent avocado browning (optional).',
      'Form small, compact oval balls of seasoned sushi rice.',
      'Wrap a strip of nori tightly around the sides of each rice ball, allowing the nori to extend slightly above the rice to form a "cup."',
      'Spoon a generous amount of the diced avocado and mango mixture onto the top of the rice within the nori cup.',
      'Serve immediately as a refreshing and visually appealing vegan gunkan sushi.'
    ]
  }
]);
const activeCategory = ref('all');
const loading = ref(false); // To simulate loading if needed
const selectedSushi = ref(null); // For the recipe popup

// Filter sushi based on active category
const filteredSushi = computed(() => {
  if (activeCategory.value === 'all') {
    return sushiData.value;
  }
  return sushiData.value.filter(sushi => sushi.category === activeCategory.value);
});

// Method to filter sushi
const filterSushi = (category) => {
  loading.value = true;
  setTimeout(() => {
    activeCategory.value = category;
    loading.value = false;
  }, 300); // Simulate a small loading delay
};

// Methods for recipe popup
const showRecipePopup = (sushi) => {
  selectedSushi.value = sushi;
  document.body.classList.add('modal-open'); // Add class to body to prevent scrolling
};

const closeRecipePopup = () => {
  selectedSushi.value = null;
  document.body.classList.remove('modal-open'); // Remove class
};

// Smooth scrolling functionality
onMounted(() => {
  document.querySelectorAll('a[href^="#"]').forEach(anchor => {
    anchor.addEventListener('click', function (e) {
      e.preventDefault();
      const targetId = this.getAttribute('href');
      const targetElement = document.querySelector(targetId);

      if (targetElement) {
        const navbarHeight = document.querySelector('.navbar')?.offsetHeight || 0;
        const offsetTop = targetElement.offsetTop - navbarHeight;

        window.scrollTo({
          top: offsetTop,
          behavior: 'smooth'
        });

        // Optional: For mobile, close the navbar if it's open
        const navLinks = document.querySelector('.nav-links');
        if (navLinks && navLinks.classList.contains('active')) {
          navLinks.classList.remove('active');
        }
      }
    });
  });

  // Handle active class for navbar links based on scroll position
  const sections = document.querySelectorAll('section[id]');
  const observerOptions = {
    root: null,
    rootMargin: '0px',
    threshold: 0.5 // Adjust as needed to control when a section becomes active
  };

  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        document.querySelectorAll('.nav-link').forEach((link) => {
          link.classList.remove('active');
        });
        const currentLink = document.querySelector(`.nav-link[href="#${entry.target.id}"]`);
        if (currentLink) {
          currentLink.classList.add('active');
        }
      }
    });
  }, observerOptions);

  sections.forEach(section => {
    observer.observe(section);
  });
});
</script>

<style>
/* Basic styling for the entire app, inherited from your base.css or global styles */
:root {
  --primary-color: #e53935; /* A red similar to your sushi cards */
  --secondary-color: #6c757d;
  --light-background: #f8f9fa;
  --dark-background: #343a40;
  --text-color: #333;
  --white-color: #fff;
  --card-background: #ffffff;
  --shadow-color: rgba(0, 0, 0, 0.1);
  --border-color: #eee;
  --highlight-color: #007bff; /* Blue for highlights */
}

body {
  font-family: 'Arial', sans-serif;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  color: var(--text-color);
  background-color: var(--light-background);
}

body.modal-open {
  overflow: hidden; /* Prevent scrolling when modal is open */
}

/* --- Navigation Bar --- */
.navbar {
  background-color: var(--card-background);
  box-shadow: 0 2px 5px var(--shadow-color);
  position: sticky;
  top: 0;
  width: 100%;
  z-index: 1000;
  padding: 10px 0;
}

.nav-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

.logo {
  font-size: 1.8em;
  font-weight: bold;
  color: var(--primary-color);
}

.nav-links {
  list-style: none;
  margin: 0;
  padding: 0;
  display: flex;
}

.nav-links li {
  margin-left: 30px;
}

.nav-link {
  text-decoration: none;
  color: var(--text-color);
  font-weight: 500;
  padding: 5px 0;
  position: relative;
  transition: color 0.3s ease;
}

.nav-link::after {
  content: '';
  position: absolute;
  left: 0;
  bottom: 0;
  width: 0;
  height: 2px;
  background-color: var(--primary-color);
  transition: width 0.3s ease;
}

.nav-link:hover,
.nav-link.active {
  color: var(--primary-color);
}

.nav-link:hover::after,
.nav-link.active::after {
  width: 100%;
}

/* --- Main Content Sections (Existing) --- */
.main-content {
  padding-top: 0; /* Adjust if navbar is fixed */
}

.hero-section {
background: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)), url('./static/flat-lay-sushi.jpg') no-repeat center center/cover;  color: var(--white-color);
  text-align: center;
  padding: 100px 20px;
  min-height: 50vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.hero-title {
  font-size: 3.5em;
  margin-bottom: 15px;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.7);
}

.hero-subtitle {
  font-size: 1.5em;
  opacity: 0.9;
}

/* Sushi Menu Section */
.sushi-menu-section {
    padding: 60px 20px;
    max-width: 1200px;
    margin: 0 auto;
}

.category-filters {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 15px;
  margin-bottom: 40px;
  padding: 20px 0;
}

.filter-btn {
  background-color: var(--card-background);
  border: 2px solid var(--border-color);
  border-radius: 25px;
  padding: 10px 25px;
  font-size: 1em;
  cursor: pointer;
  transition: all 0.3s ease;
  color: var(--text-color);
  font-weight: 500;
}

.filter-btn:hover {
  background-color: var(--primary-color);
  color: var(--white-color);
  border-color: var(--primary-color);
}

.filter-btn.active {
  background-color: var(--primary-color);
  color: var(--white-color);
  border-color: var(--primary-color);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.sushi-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 30px;
  position: relative; /* For loading overlay */
}

.sushi-container.loading::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(255, 255, 255, 0.7);
  z-index: 10;
  display: flex;
  justify-content: center;
  align-items: center;
  /* You can add a spinner here if you wish */
}

.sushi-card {
  background-color: var(--card-background);
  border-radius: 15px;
  box-shadow: 0 4px 15px var(--shadow-color);
  overflow: hidden;
  text-align: center;
  padding: 25px;
  display: flex;
  flex-direction: column;
  align-items: center;
  cursor: pointer;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  position: relative;
}

.sushi-card:hover {
  transform: translateY(-8px);
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
}

.category-badge {
  position: absolute;
  top: 15px;
  right: 15px;
  background-color: var(--primary-color);
  color: var(--white-color);
  padding: 5px 12px;
  border-radius: 15px;
  font-size: 0.85em;
  font-weight: bold;
}

.sushi-stack {
  position: relative;
  width: 150px;
  height: 80px;
  margin-bottom: 20px;
}

.rice-base {
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 120px;
  height: 40px;
  background-color: #f0f0f0;
  border-radius: 20px 20px 10px 10px / 20px 20px 5px 5px;
  box-shadow: inset 0 -3px 5px rgba(0, 0, 0, 0.1);
}

.sashimi {
  position: absolute;
  top: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 140px;
  height: 50px;
  border-radius: 25px 25px 0 0 / 25px 25px 0 0;
  box-shadow: 0 3px 8px rgba(0, 0, 0, 0.15);
}

/* Specific sashimi colors (adjust as needed) */
.sashimi.tuna { background-color: #FF6347; }
.sashimi.salmon { background-color: #FFA07A; }
.sashimi.california { background-color: #F0E68C; } /* Example for a California roll "top" */
.sashimi.tuna-sashimi { background-color: #FF6347; }
.sashimi.avocado { background-color: #9ACD32; }
.sashimi.shrimp { background-color: #FF8C00; }


.sushi-name {
  font-size: 1.5em;
  font-weight: bold;
  margin-bottom: 10px;
  color: var(--primary-color);
}

.sushi-description {
  font-size: 0.95em;
  color: #666;
  margin-bottom: 15px;
  flex-grow: 1; /* Allows description to take available space */
}

.ingredients {
  margin-top: 10px;
  margin-bottom: 20px;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 8px;
}

.ingredient-tag {
  background-color: #e0e0e0;
  color: #555;
  padding: 5px 12px;
  border-radius: 15px;
  font-size: 0.8em;
  white-space: nowrap;
}

.add-to-cart {
  background-color: var(--primary-color);
  color: var(--white-color);
  border: none;
  border-radius: 25px;
  padding: 12px 25px;
  font-size: 1em;
  cursor: pointer;
  transition: background-color 0.3s ease, transform 0.2s ease;
  width: 100%; /* Make button full width of card */
  max-width: 200px;
  font-weight: bold;
}

.add-to-cart:hover {
  background-color: #c0392b;
  transform: translateY(-2px);
}

/* Modal Styles */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.7);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1001;
  backdrop-filter: blur(5px);
}

.modal-content {
  background-color: var(--card-background);
  padding: 40px;
  border-radius: 15px;
  max-width: 700px;
  width: 90%;
  position: relative;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
  max-height: 90vh; /* Limit modal height */
  overflow-y: auto; /* Enable scrolling within modal */
}

.close-modal {
  position: absolute;
  top: 15px;
  right: 20px;
  background: none;
  border: none;
  font-size: 2em;
  color: #555;
  cursor: pointer;
  transition: color 0.3s ease;
}

.close-modal:hover {
  color: var(--primary-color);
}

.modal-content h2 {
  font-size: 2em;
  color: var(--primary-color);
  margin-bottom: 15px;
  text-align: center;
}

.modal-description {
  font-size: 1.1em;
  color: #666;
  margin-bottom: 25px;
  text-align: center;
}

.modal-recipe-details h3 {
  font-size: 1.4em;
  color: var(--text-color);
  margin-top: 20px;
  margin-bottom: 10px;
  border-bottom: 2px solid var(--border-color);
  padding-bottom: 5px;
}

.modal-ingredients-list,
.modal-instructions-list {
  list-style-type: none;
  padding: 0;
  margin-bottom: 20px;
}

.modal-ingredients-list li,
.modal-instructions-list li {
  background-color: #f9f9f9;
  border-left: 5px solid var(--primary-color);
  padding: 10px 15px;
  margin-bottom: 8px;
  border-radius: 5px;
  line-height: 1.5;
  color: #444;
}

.modal-instructions-list li {
  counter-increment: instruction-counter;
  position: relative;
  padding-left: 35px; /* Space for counter */
}

.modal-instructions-list li::before {
  content: counter(instruction-counter) ".";
  position: absolute;
  left: 10px;
  font-weight: bold;
  color: var(--primary-color);
}

/* --- New Sections Styling --- */
.content-section {
  padding: 80px 20px;
  background-color: var(--white-color);
  border-bottom: 1px solid var(--border-color);
}

.content-section.light-background {
  background-color: var(--light-background);
}

.content-wrapper {
  max-width: 1000px;
  margin: 0 auto;
}

.section-title {
  font-size: 2.5em;
  color: var(--primary-color);
  text-align: center;
  margin-bottom: 20px;
}

.section-subtitle {
  font-size: 1.2em;
  color: #666;
  text-align: center;
  margin-bottom: 50px;
  line-height: 1.6;
}

.subsection-title {
  font-size: 1.8em;
  color: var(--text-color);
  margin-top: 40px;
  margin-bottom: 20px;
  border-bottom: 2px solid var(--border-color);
  padding-bottom: 5px;
}

.info-list {
  list-style: none;
  padding: 0;
  margin-bottom: 30px;
}

.info-list li {
  background-color: var(--card-background);
  border: 1px solid var(--border-color);
  border-left: 5px solid var(--highlight-color);
  padding: 15px 20px;
  margin-bottom: 10px;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
}

.info-list li ul {
  margin-top: 10px;
  padding-left: 20px;
  list-style: disc;
  color: #555;
}

.text-link {
  color: var(--primary-color);
  text-decoration: none;
  font-weight: 500;
}

.text-link:hover {
  text-decoration: underline;
}

.note-text {
  font-size: 0.9em;
  color: #888;
  margin-top: 40px;
  padding: 15px;
  background-color: #fff3cd; /* Light warning yellow */
  border-left: 5px solid #ffc107; /* Warning yellow */
  border-radius: 8px;
}

/* Exhibition Specific Styling */
.exhibition-details-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 40px;
  align-items: center;
}

@media (min-width: 768px) {
  .exhibition-details-grid {
    grid-template-columns: 1fr 1fr;
  }
}

.exhibition-image-container {
  text-align: center;
}

.exhibition-image {
  max-width: 100%;
  height: auto;
  border-radius: 10px;
  box-shadow: 0 8px 20px var(--shadow-color);
}

.exhibition-text-content {
  padding: 15px 0;
}

.highlight-text {
  color: var(--primary-color);
  font-weight: bold;
}

.link-heading {
  font-size: 1.5em;
  color: var(--text-color);
  margin-top: 30px;
  margin-bottom: 15px;
}

.link-description {
  font-size: 1.1em;
  line-height: 1.6;
  margin-bottom: 20px;
}

.action-button {
  display: inline-block;
  padding: 12px 25px;
  border-radius: 25px;
  text-decoration: none;
  font-weight: bold;
  transition: all 0.3s ease;
  text-align: center;
  margin-right: 15px;
  margin-bottom: 15px; /* For mobile stacking */
}

.primary-button {
  background-color: var(--primary-color);
  color: var(--white-color);
  border: 2px solid var(--primary-color);
}

.primary-button:hover {
  background-color: #c0392b;
  border-color: #c0392b;
  transform: translateY(-2px);
}

.secondary-button {
  background-color: transparent;
  color: var(--secondary-color);
  border: 2px solid var(--secondary-color);
}

.secondary-button:hover {
  background-color: var(--secondary-color);
  color: var(--white-color);
  transform: translateY(-2px);
}

/* Footer */
.footer {
  background-color: var(--dark-background);
  color: var(--white-color);
  text-align: center;
  padding: 30px 20px;
  margin-top: 50px;
  font-size: 0.9em;
}

/* --- Responsive Adjustments --- */
@media (max-width: 768px) {
  .nav-links {
    display: none; /* Hide for now, you'd implement a mobile toggle */
    flex-direction: column;
    width: 100%;
    text-align: center;
  }
  .nav-links.active {
    display: flex;
  }
  .nav-links li {
    margin: 10px 0;
  }

  .hero-title {
    font-size: 2.5em;
  }

  .hero-subtitle {
    font-size: 1.2em;
  }

  .category-filters {
    gap: 10px;
  }

  .filter-btn {
    padding: 8px 20px;
    font-size: 0.9em;
  }

  .sushi-card {
    padding: 20px;
  }

  .modal-content {
    width: 95%;
    padding: 25px;
  }

  .section-title {
    font-size: 2em;
  }

  .section-subtitle {
    font-size: 1em;
    margin-bottom: 30px;
  }

  .subsection-title {
    font-size: 1.5em;
  }

  .action-button {
    width: 100%; /* Full width buttons on small screens */
    margin-right: 0;
  }
}
</style>