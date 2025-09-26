<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>The Midnight Quill - Interactive Menu</title>
    <!-- Chosen Palette: Earthy & Elegant -->
    <!-- Application Structure Plan: A dashboard-style application featuring a primary interactive filter navigation (All, Cocktails, Wine, Beer) that dynamically updates a grid of drink cards. This structure was chosen to provide users with immediate control and a clear, focused view of their desired category, which is more intuitive than scrolling through a long, static menu. The user flow is simple: land, see all, filter with one click, explore. An additional section with data visualizations provides a high-level summary of the menu's composition and pricing to add analytical depth and visual appeal. -->
    <!-- Visualization & Content Choices: 
        1. Drink Menu -> Goal: Organize/Inform -> Viz: Interactive Card Grid with Filters -> Interaction: Click filters to update grid -> Justification: Allows users to easily find specific types of drinks without being overwhelmed by the full list. Method: HTML/CSS/JS.
        2. Menu Composition -> Goal: Inform (Proportion) -> Viz: Donut Chart -> Interaction: Hover to see details -> Justification: Best way to show the part-to-whole relationship of drink categories. Library: Chart.js/Canvas.
        3. Price Comparison -> Goal: Compare -> Viz: Sorted Horizontal Bar Chart -> Interaction: Hover to see details -> Justification: Clearly compares the prices of all individual items and allows users to identify drinks within their budget. Library: Chart.js/Canvas. -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@400;600;700&family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
    <style>
        body {
            background-color: #FDFBF5;
            font-family: 'Poppins', sans-serif;
            color: #40312C;
        }
        h1, h2, h3, h4 {
            font-family: 'Cormorant Garamond', serif;
        }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 800px;
            margin-left: auto;
            margin-right: auto;
            height: 350px;
            max-height: 500px;
        }
        .nav-btn {
            transition: all 0.3s ease;
        }
        .nav-btn.active {
            background-color: #A38D64;
            color: #FFFFFF;
        }
        .drink-card {
             background-color: #FFFFFF;
             border-left: 4px solid transparent;
             transition: all 0.3s ease;
        }
        .drink-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
            border-left-color: #A38D64;
        }
    </style>
</head>
<body class="antialiased">

    <div class="container mx-auto p-4 md:p-8">

        <header class="text-center my-12 md:my-16">
            <h1 class="text-5xl md:text-7xl font-bold text-[#40312C]">The Midnight Quill</h1>
            <p class="text-lg md:text-xl text-gray-600 mt-2">Interactive & Curated Libations Menu</p>
        </header>

        <nav class="flex justify-center items-center gap-2 md:gap-4 mb-12 flex-wrap">
            <button id="filter-all" class="nav-btn active text-lg font-semibold py-2 px-6 rounded-full" data-filter="all">All Drinks</button>
            <button id="filter-cocktail" class="nav-btn text-lg font-semibold py-2 px-6 rounded-full" data-filter="cocktail">Cocktails</button>
            <button id="filter-wine" class="nav-btn text-lg font-semibold py-2 px-6 rounded-full" data-filter="wine">Wines</button>
            <button id="filter-beer" class="nav-btn text-lg font-semibold py-2 px-6 rounded-full" data-filter="beer">Beers</button>
        </nav>

        <main id="drink-grid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8 mb-16">
        </main>

        <section class="bg-white/60 rounded-lg shadow-xl p-6 md:p-8 my-16">
             <div class="text-center mb-8">
                <h2 class="text-4xl font-bold">Menu at a Glance</h2>
                <p class="mt-2 text-gray-600">Visual insights into our collection's composition and pricing.</p>
            </div>
            <div class="grid grid-cols-1 lg:grid-cols-5 gap-8 items-center">
                <div class="lg:col-span-2">
                     <h3 class="text-2xl font-bold mb-4 text-center">Drink Category Breakdown</h3>
                    <p class="text-center mb-4 text-gray-600">Cocktails represent the largest portion of our offerings, showcasing our focus on mixology.</p>
                    <div class="chart-container" style="height: 300px;">
                        <canvas id="menuCompositionChart"></canvas>
                    </div>
                </div>
                <div class="lg:col-span-3">
                    <h3 class="text-2xl font-bold mb-4 text-center">Price Distribution Across the Menu</h3>
                    <p class="text-center mb-4 text-gray-600">From an accessible beer to our most premium cocktail, this chart displays the price for every item we serve, sorted for your convenience.</p>
                    <div class="chart-container" style="height: 450px;">
                        <canvas id="priceDistributionChart"></canvas>
                    </div>
                </div>
            </div>
        </section>

    </div>

    <footer class="text-center py-8 text-gray-500">
        <p>The Midnight Quill &copy; 2025. Experience craft and curation in every glass.</p>
    </footer>

    <script>
        const drinksData = [
            { name: "The Velvet Serpent", description: "A smooth and smoky blend of mezcal, blackberry liqueur, fresh lime juice, and a hint of ginger.", price: 14, category: "cocktail", subCategory: "Signature" },
            { name: "The Lumina Spark", description: "A bright and effervescent concoction of gin, elderflower liqueur, sparkling rosé, and a splash of grapefruit juice.", price: 12, category: "cocktail", subCategory: "Signature" },
            { name: "The Autumn's Embrace", description: "Warm and spicy. A bourbon-based drink with spiced apple cider, a dash of cinnamon simple syrup, and a squeeze of lemon.", price: 13, category: "cocktail", subCategory: "Signature" },
            { name: "Old Fashioned", description: "The timeless classic. Your choice of bourbon or rye, muddled with sugar and bitters, and garnished with an orange peel.", price: 11, category: "cocktail", subCategory: "Classic" },
            { name: "Martini", description: "Shaken or stirred. Dry gin or vodka with a whisper of vermouth. Olive or lemon twist.", price: 12, category: "cocktail", subCategory: "Classic" },
            { name: "Margarita", description: "Crisp and refreshing. Tequila, fresh lime juice, and Cointreau. Served on the rocks with a salted rim.", price: 10, category: "cocktail", subCategory: "Classic" },
            { name: "Negroni", description: "A perfect balance of bitter and sweet. Gin, Campari, and sweet vermouth.", price: 11, category: "cocktail", subCategory: "Classic" },
            { name: "Sauvignon Blanc", description: "A crisp and zesty white with notes of citrus and green apple.", price: 9, priceBottle: 34, category: "wine", subCategory: "White" },
            { name: "Chardonnay", description: "A full-bodied wine with a buttery finish and hints of vanilla.", price: 10, priceBottle: 38, category: "wine", subCategory: "White" },
            { name: "Pinot Noir", description: "Light and delicate, with aromas of cherry and earthy undertones.", price: 11, priceBottle: 42, category: "wine", subCategory: "Red" },
            { name: "Cabernet Sauvignon", description: "Bold and rich, featuring notes of black currant and a strong tannic structure.", price: 12, priceBottle: 45, category: "wine", subCategory: "Red" },
            { name: "Lager (Local)", description: "Light, crisp, and easy to drink.", price: 7, category: "beer" },
            { name: "IPA (India Pale Ale)", description: "A hoppy and bitter ale with a citrus aroma.", price: 8, category: "beer" },
            { name: "Stout", description: "A dark, rich beer with notes of roasted coffee and chocolate.", price: 8, category: "beer" }
        ];

        const drinkGrid = document.getElementById('drink-grid');
        const filterButtons = document.querySelectorAll('.nav-btn');

        const renderDrinks = (filter = 'all') => {
            drinkGrid.innerHTML = '';
            const filteredDrinks = drinksData.filter(drink => filter === 'all' || drink.category === filter);

            filteredDrinks.forEach(drink => {
                let priceInfo = `<p class="text-2xl font-bold text-[#A38D64]">$${drink.price}</p>`;
                if (drink.category === 'wine') {
                    priceInfo = `<div class="text-right"><p class="text-xl font-semibold text-[#A38D64]">Glass: $${drink.price}</p><p class="text-md text-gray-500">Bottle: $${drink.priceBottle}</p></div>`;
                }

                const card = `
                    <div class="drink-card rounded-lg shadow-md p-6 flex flex-col justify-between">
                        <div>
                            <div class="flex justify-between items-start">
                                <h3 class="text-2xl font-bold mb-2">${drink.name}</h3>
                                ${priceInfo}
                            </div>
                            <p class="text-gray-600">${drink.description}</p>
                        </div>
                        <div class="text-left mt-4">
                            <span class="text-sm font-semibold text-white ${drink.category === 'cocktail' ? 'bg-blue-500' : drink.category === 'wine' ? 'bg-red-800' : 'bg-yellow-700'} py-1 px-3 rounded-full">${drink.subCategory || drink.category}</span>
                        </div>
                    </div>
                `;
                drinkGrid.innerHTML += card;
            });
        };

        filterButtons.forEach(button => {
            button.addEventListener('click', () => {
                const filter = button.dataset.filter;
                
                filterButtons.forEach(btn => btn.classList.remove('active'));
                button.classList.add('active');
                
                renderDrinks(filter);
            });
        });
        
        document.addEventListener('DOMContentLoaded', () => {
            renderDrinks('all');

            const tooltipTitleCallback = (tooltipItems) => {
                const item = tooltipItems[0];
                let label = item.chart.data.labels[item.dataIndex];
                if (Array.isArray(label)) { return label.join(' '); } 
                else { return label; }
            };

            const chartColors = {
                darkBrown: '#40312C',
                tan: '#A38D64',
                olive: '#6A7B53',
                lightTan: '#D7B07E',
                cream: '#FDFBF5'
            };

            const chartPluginOptions = {
                legend: { labels: { color: chartColors.darkBrown, font: { family: "'Poppins', sans-serif", size: 14 } } },
                tooltip: { callbacks: { title: tooltipTitleCallback }, bodyFont: { family: "'Poppins', sans-serif" }, titleFont: { family: "'Poppins', sans-serif", weight: 'bold' } }
            };
            
            const chartScaleOptions = (color) => ({
                ticks: { color: color, font: { family: "'Poppins', sans-serif" } },
                grid: { color: 'rgba(64, 49, 44, 0.1)' }
            });

            new Chart(document.getElementById('menuCompositionChart'), {
                type: 'doughnut',
                data: {
                    labels: ['Cocktails', 'Wines', 'Beers'],
                    datasets: [{
                        label: 'Number of Drinks',
                        data: [
                            drinksData.filter(d => d.category === 'cocktail').length,
                            drinksData.filter(d => d.category === 'wine').length,
                            drinksData.filter(d => d.category === 'beer').length
                        ],
                        backgroundColor: [chartColors.tan, chartColors.olive, chartColors.darkBrown],
                        borderColor: chartColors.cream,
                        borderWidth: 4
                    }]
                },
                options: { responsive: true, maintainAspectRatio: false, plugins: { ...chartPluginOptions } }
            });
            
            const sortedDrinks = [...drinksData].sort((a, b) => a.price - b.price);
            new Chart(document.getElementById('priceDistributionChart'), {
                type: 'bar',
                data: {
                    labels: sortedDrinks.map(d => d.name),
                    datasets: [{
                        label: 'Price ($)',
                        data: sortedDrinks.map(d => d.price),
                        backgroundColor: chartColors.tan,
                        borderColor: chartColors.darkBrown,
                        borderWidth: 1,
                        borderRadius: 4
                    }]
                },
                options: {
                    indexAxis: 'y',
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        x: { ...chartScaleOptions(chartColors.darkBrown), beginAtZero: true },
                        y: { ...chartScaleOptions(chartColors.darkBrown) }
                    },
                    plugins: { ...chartPluginOptions, legend: { display: false } }
                }
            });
        });

    </script>
</body>
</html>
