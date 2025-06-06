<script lang="ts">
    import { onMount } from 'svelte';
    import { page } from '$app/stores';
    import type { PageData } from './$types';

    // export let data: PageData;

    let currentRecipe = $state(null);

let recipes = $state([
    { 
        title: 'Steak Avocado',
        ingredients: [
            { name: 'Baby Gem Lettuce', qty: '1/2 head', station: 1 },
            { name: 'Romaine Lettuce', qty: '2 oz', station: 1 },
            { name: 'Black Beans', qty: '1', station: 1 },
            { name: 'Cut Corn', qty: '1/4 cup', station: 2 },
            { name: 'Grape Tomatoes', qty: '1/4', station: 2 },
            { name: 'Jalapeno Ranch Dressing', qty: '1/4', station: 2 },
            { name: 'Avocado', qty: '1/2', station: 2 },
            { name: 'Sirloin Steak', qty: '1 ea', station: 2 },
            { name: 'Tortilla Strips', qty: '1.5 oz', station: 2 },
            { name: 'Maldon Salt', qty: '.5 tsp', station: 2 },
            { name: 'Micro Babes', qty: '.1 oz', station: 2 },

        ],
        plating: [
            { instruction: "Slice steak against the grain", station: 2 },
            { instruction: "Arrange avocado slices around plate", station: 1 }, 
            { instruction: "Top with thinly sliced red onion", station: 2 },
            { instruction: "Garnish with cilantro leaves", station: 2 },
            { instruction: "Drizzle with lime juice", station: 2 }
        ],
        created: "2023-05-15"
    },
    { 
        title: 'Ceasar Salad',
        ingredients: [
            { name: 'romaine lettuce', qty: '9 oz', station: 1 },
            { name: 'Parmesan cheese', qty: 'yellow scoop', station: 1 },
            { name: 'croutons', qty: '10 ea', station: 1 },
            { name: 'Caesar dressing', qty: '2 oz', station: 1 }
        ],
        plating: [
            { instruction: "Chop romaine into bite-sized pieces", station: 1 },
            { instruction: "Toss with dressing in a large bowl", station: 1 },
            { instruction: "Transfer to serving plate", station: 1 },
            { instruction: "Top with croutons and shaved Parmesan", station: 1 },
            { instruction: "Finish with lemon wedge on side", station: 1 }
        ],
        created: "2023-02-10"
    },
    { 
        title: 'Garden Crunch',
        ingredients: [
            { name: 'mixed greens', qty: '4 cups', station: 1 },
            { name: 'cucumber', qty: '1', station: 1 },
            { name: 'cherry tomatoes', qty: '1 cup', station: 1 },
            { name: 'carrots', qty: '2', station: 1 },
            { name: 'balsamic vinaigrette', qty: '3 tbsp', station: 1 }
        ],
        plating: [
            { instruction: "Create a base with mixed greens", station: 2 },
            { instruction: "Arrange cucumber ribbons around edges", station: 2 },
            { instruction: "Place halved cherry tomatoes in center", station: 2 },
            { instruction: "Add carrot ribbons on top", station: 2 },
            { instruction: "Drizzle vinaigrette in zigzag pattern", station: 2 }
        ],
        created: "2023-04-22"
    },
    { 
        title: 'Thai Chicken',
        ingredients: [
            { name: 'chicken breast', qty: '1 lb', station: 4 }, // grill
            { name: 'peanut sauce', qty: '1/2 cup', station: 1 }, // pantry
            { name: 'bell peppers', qty: '2', station: 1 }, // pantry
            { name: 'basil', qty: '1/4 cup', station: 1 }, // pantry
            { name: 'rice', qty: '2 cups cooked', station: 3 } // oven
        ],
        plating: [
            { instruction: "Scoop rice into bowl as base", station: 2 }, // prep
            { instruction: "Arrange sliced chicken on one side", station: 2 }, // prep
            { instruction: "Place bell pepper strips on other side", station: 2 }, // prep
            { instruction: "Drizzle peanut sauce over everything", station: 2 }, // prep
            { instruction: "Garnish with fresh basil leaves", station: 2 } // prep
        ],
        created: "2023-06-18"
    },
    { 
        title: 'Creamy Burrata',
        ingredients: [
            { name: 'burrata cheese', qty: '8 oz', station: 1 }, // pantry
            { name: 'heirloom tomatoes', qty: '2', station: 1 }, // pantry
            { name: 'basil', qty: '1/4 cup', station: 1 }, // pantry
            { name: 'olive oil', qty: '2 tbsp', station: 1 }, // pantry
            { name: 'balsamic glaze', qty: '1 tbsp', station: 1 } // pantry
        ],
        plating: [
            { instruction: "Arrange tomato slices in circular pattern", station: 2 }, // prep
            { instruction: "Place whole burrata in center", station: 2 }, // prep
            { instruction: "Drizzle with olive oil and balsamic", station: 2 }, // prep
            { instruction: "Scatter fresh basil leaves", station: 2 }, // prep
            { instruction: "Add cracked black pepper on top", station: 2 } // prep
        ],
        created: "2023-03-05"
    },
    { 
        title: 'Simple Salad',
        ingredients: [
            { name: 'mixed greens', qty: '4 cups', station: 1 }, // pantry
            { name: 'cucumber', qty: '1/2', station: 1 }, // pantry
            { name: 'red wine vinaigrette', qty: '2 tbsp', station: 1 }, // pantry
            { name: 'salt', qty: 'to taste', station: 1 }, // pantry
            { name: 'pepper', qty: 'to taste', station: 1 } // pantry
        ],
        plating: [
            { instruction: "Pile greens high in center of plate", station: 2 }, // prep
            { instruction: "Arrange cucumber slices around edges", station: 2 }, // prep
            { instruction: "Lightly dress with vinaigrette", station: 2 }, // prep
            { instruction: "Season with salt and pepper", station: 2 }, // prep
            { instruction: "Serve immediately", station: 2 } // prep
        ],
        created: "2023-01-12"
    },
    { 
        title: 'Chopped Greek',
        ingredients: [
            { name: 'romaine lettuce', qty: '4 cups', station: 1 }, // pantry
            { name: 'feta cheese', qty: '1/2 cup', station: 1 }, // pantry
            { name: 'kalamata olives', qty: '1/4 cup', station: 1 }, // pantry
            { name: 'red onion', qty: '1/4', station: 1 }, // pantry
            { name: 'Greek dressing', qty: '3 tbsp', station: 1 } // pantry
        ],
        plating: [
            { instruction: "Chop all ingredients uniformly", station: 2 }, // prep
            { instruction: "Mix in large bowl with dressing", station: 2 }, // prep
            { instruction: "Pack into small bowl then invert onto plate", station: 2 }, // prep
            { instruction: "Sprinkle extra feta on top", station: 2 }, // prep
            { instruction: "Add whole olives as garnish", station: 2 } // prep
        ],
        created: "2023-07-30"
    },
    { 
        title: 'Whipped Feta Dip',
        ingredients: [
            { name: 'feta cheese', qty: '8 oz', station: 1 }, // pantry
            { name: 'cream cheese', qty: '4 oz', station: 1 }, // pantry
            { name: 'olive oil', qty: '1 tbsp', station: 1 }, // pantry
            { name: 'lemon juice', qty: '1 tbsp', station: 1 }, // pantry
            { name: 'garlic', qty: '1 clove', station: 1 } // pantry
        ],
        plating: [
            { instruction: "Spoon dip into shallow serving bowl", station: 2 }, // prep
            { instruction: "Use back of spoon to create swirls", station: 2 }, // prep
            { instruction: "Drizzle with olive oil", station: 2 }, // prep
            { instruction: "Sprinkle with chili flakes or herbs", station: 2 }, // prep
            { instruction: "Serve with pita chips or vegetables", station: 2 } // prep
        ],
        created: "2023-08-14"
    },
    { 
        title: 'Ahi Tuna Bowl',
        ingredients: [
            { name: 'ahi tuna', qty: '1 lb', station: 2 }, // prep
            { name: 'sushi rice', qty: '2 cups cooked', station: 3 }, // oven
            { name: 'avocado', qty: '1', station: 1 }, // pantry
            { name: 'cucumber', qty: '1/2', station: 1 }, // pantry
            { name: 'sesame seeds', qty: '1 tbsp', station: 1 } // pantry
        ],
        plating: [
            { instruction: "Press rice into bottom of bowl", station: 2 }, // prep
            { instruction: "Arrange sliced tuna in fan pattern", station: 2 }, // prep
            { instruction: "Add avocado and cucumber slices", station: 2 }, // prep
            { instruction: "Sprinkle with sesame seeds", station: 2 }, // prep
            { instruction: "Serve with soy sauce and wasabi", station: 2 } // prep
        ],
        created: "2023-09-05"
    },
    { 
        title: 'Guacamole',
        ingredients: [
            { name: 'avocado', qty: '3', station: 1 }, // pantry
            { name: 'lime', qty: '1', station: 1 }, // pantry
            { name: 'red onion', qty: '1/4 cup', station: 1 }, // pantry
            { name: 'cilantro', qty: '2 tbsp', station: 1 }, // pantry
            { name: 'salt', qty: 'to taste', station: 1 } // pantry
        ],
        plating: [
            { instruction: "Scoop guacamole into stone mortar", station: 2 }, // prep
            { instruction: "Create small well in center", station: 2 }, // prep
            { instruction: "Add lime wedge to side", station: 2 }, // prep
            { instruction: "Garnish with cilantro sprig", station: 2 }, // prep
            { instruction: "Serve with tortilla chips", station: 2 } // prep
        ],
        created: "2023-10-22"
    },
    { 
        title: 'Birthday Cake Donuts',
        sizes:['regular', 'Large'],
        ingredients: [
            { name: 'Birthday Cake Donut', qty: '12 ea', station: 2 }, 
            { name: 'Unsalted Butter Solids Cabot 620', qty: '2 oz', comment: 'Melted', station: 2 }, 
            { name: 'Lemon Sugar Prep', qty: '4 Tbsp', station: 2 }, 
            { name: 'White chocolate glaze prep', qty: '3 Oz', station: 0 },
            { name: 'Sprinkles, Rainbow', qty: '.1 oz', comment: 'pinch', station: 0 } 
        ],
        plating: [
            { instruction: "Reheat the Birthday Cake Donuts in the oven at 350F until warm. ~2 minutes.", station: 2 },
            { instruction: "Take donuts out of the oven then immediately toss for 1 second into warm melted butter. *Toss only 1 second, too long will make them soggy.", station: 2 },
            { instruction: "Toss donuts immediately in Lemon Sugar using mixing bowl.", station: 2 },
            { instruction: "Put coated donutes in the branded bag and place on small green plate, logo side up. Donuts should tumble out of bag.", station: 2 },
            { instruction: "Add black napkin to the other side of the plate. Fill a ramekin with white chocolate glaze and place on the plate, on the top of the napkin.", station: 0 }, 
            { instruction: "Sprinkle white chocolate glaze with rainbow sprinkles.", station: 0 } 
        ],
        created: "2025-1-14",
        Edited: "2025-1-19",
    },
    { 
        title: 'Flourless Chocolate Cake',
        ingredients: [
            { name: 'dark chocolate', qty: '8 oz', station: 1 }, // pantry
            { name: 'butter', qty: '1/2 cup', station: 1 }, // pantry
            { name: 'eggs', qty: '4', station: 1 }, // pantry
            { name: 'sugar', qty: '3/4 cup', station: 1 }, // pantry
            { name: 'cocoa powder', qty: '1/4 cup', station: 1 } // pantry
        ],
        plating: [
            { instruction: "Dust plate with cocoa powder first", station: 2 }, // prep
            { instruction: "Place cake slice slightly off-center", station: 2 }, // prep
            { instruction: "Add fresh berries alongside", station: 2 }, // prep
            { instruction: "Drizzle chocolate sauce decoratively", station: 2 }, // prep
            { instruction: "Top with quenelle of whipped cream", station: 2 } // prep
        ],
        created: "2023-12-25"
    },
    { 
        title: 'Birthday Cake',
        ingredients: [
            { name: 'flour', qty: '2 1/2 cups', station: 1 }, // pantry
            { name: 'sugar', qty: '1 1/2 cups', station: 1 }, // pantry
            { name: 'eggs', qty: '3', station: 1 }, // pantry
            { name: 'butter', qty: '1 cup', station: 1 }, // pantry
            { name: 'vanilla extract', qty: '1 tbsp', station: 1 } // pantry
        ],
        plating: [
            { instruction: "Place on decorative cake stand", station: 2 }, // prep
            { instruction: "Arrange candles as desired", station: 2 }, // prep
            { instruction: "Add fresh flowers around base", station: 2 }, // prep
            { instruction: "Use piping for message", station: 2 }, // prep
            { instruction: "Serve with ice cream", station: 2 } // prep
        ],
        created: "2023-01-01"
    },
    { 
        title: 'Cookie skillet',
        ingredients: [
            { name: 'flour', qty: '1 1/2 cups', station: 1 }, // pantry
            { name: 'chocolate chips', qty: '1 cup', station: 1 }, // pantry
            { name: 'butter', qty: '1/2 cup', station: 1 }, // pantry
            { name: 'brown sugar', qty: '1/2 cup', station: 1 }, // pantry
            { name: 'egg', qty: '1', station: 1 } // pantry
        ],
        plating: [
            { instruction: "Serve warm in skillet", station: 2 }, // prep
            { instruction: "Top with scoop of vanilla ice cream", station: 2 }, // prep
            { instruction: "Drizzle with caramel sauce", station: 2 }, // prep
            { instruction: "Sprinkle with sea salt", station: 2 }, // prep
            { instruction: "Provide small spoons for sharing", station: 2 } // prep
        ],
        created: "2023-02-14"
    }
]);
let shownRecipes = $state([]);
let searchRecipe = $state([]);
let stations = $state([
    { 
        name: 'pantry',
        color: '#8D6E63',  // Warm brown (like wood shelves)
        textColor: '#FFFFFF' // White text for contrast
    },
    { 
        name: 'prep',
        color: '#4CAF50',   // Fresh green (like cutting boards)
        textColor: '#000000' // Black text for contrast
    },
    { 
        name: 'oven',
        color: '#F44336',   // Alert red (for heat warning)
        textColor: '#FFFFFF' // White text
    },
    { 
        name: 'stove',
        color: '#FF9800',   // Orange (burner flames)
        textColor: '#000000' // Black text
    },
    { 
        name: 'grill',
        color: '#795548',   // Dark brown (grill marks)
        textColor: '#FFFFFF' // White text
    },
    { 
        name: 'fryer',
        color: '#FFC107',   // Golden yellow (fried food)
        textColor: '#000000' // Black text
    },
    { 
        name: 'saute',
        color: '#9C27B0',   // Purple (distinct from other stations)
        textColor: '#FFFFFF' // White text
    }
]);

$effect(() => {

    shownRecipes = recipes.filter(recipe => {
        const searchTerm = searchRecipe;
        return recipe.title.toLowerCase().includes(searchTerm) || 
               recipe.ingredients.some(ingredient => ingredient.name.toLowerCase().includes(searchTerm));
    });
});

    onMount(() => {
        shownRecipes = recipes;
    });
</script>

<div class="flex flex-col bg-gray-100">

    <div class="flex flex-row items-center justify-center w-full bg-gray-200 p-6 rounded shadow-lg">
        <div class="flex-1">

            <h1 class="text-2xl font-bold">
                {#if currentRecipe}
                    {currentRecipe.title}
                {:else}
                    Recipe Book
                {/if}
            </h1>
        </div>
        {#if currentRecipe}
        <div class="flex gap-2">
            <button class="bg-red-500 text-white p-2 rounded cursor-pointer hover:bg-red-600" onclick={() => currentRecipe = null}>Back to Recipes</button>
            <button class="bg-green-500 text-white p-2 rounded cursor-pointer hover:bg-green-600">Edit Recipe</button>

        </div>
        {:else}
        <button class="bg-blue-500 text-white p-2 rounded" onclick={() => navigate('/recipes/new')}>Add New Recipe</button>

        {/if}
    </div>
    {#if currentRecipe}
        <div class="flex flex-col bg-white p-4 rounded shadow-md mb-4 w-full">
            <h3>Created: {currentRecipe.created}</h3>
            <div class="mb-4">
                <strong>Ingredients:</strong>
                <ul>
                    {#each currentRecipe.ingredients as ingredient}
                        <li>{ingredient.name} - {ingredient.qty}</li>
                    {/each}
                </ul>
            </div>
            <div>
                <strong>Plating Instructions:</strong>
                <ol class="list-decimal pl-4">
                    {#each currentRecipe.plating as step}
                        <li style={`color: ${stations[step.station].color};`} >{step.instruction}</li>
                    {/each}
                </ol>
            </div>
        </div>
        {:else}
        <div class="flex flex-row items-center justify-between bg-white p-4 rounded shadow-md mb-4 w-full gap-2">
          <div class="flex-1">
            <input bind:value={searchRecipe} type="text" placeholder="Search recipes..." class="w-full p-2 border rounded" />
        </div>

        <button class="bg-blue-500 text-white p-2 rounded">Search</button>
    </div>

    <div class="flex flex-row gap-2 items-center bg-white p-4 rounded shadow-md mb-4 w-full flex-wrap">

  
    {#each shownRecipes as recipe}
        <button class="w-[33%] hover:bg-slate-400 bg-slate-200 p-4 rounded cursor-pointer h-[200px]" onclick={() => {currentRecipe = recipe;}}>
            <div class="text-lg font-semibold mb-3 border-b">{recipe.title}</div>
            <div class="flex flex-row">

            <div class="flex-1 flex justify-left items-start flex-col p-2">
            {#each recipe.ingredients as ingredient}
                <div style={`color: ${stations[ingredient.station].color};`} class={`text-sm`}><strong>{ingredient.name}</strong> &ndash;{ingredient.qty}</div>
            {/each}
            </div>

            <div class="bg-slate-500 flex-1">test</div>
            </div>
        </button>
    {/each}

    </div>
    {/if}

    

</div>