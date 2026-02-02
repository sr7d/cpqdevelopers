---
layout: post
title: CPQ Price Waterfall Calculator
description: This calculator simulates Salesforce CPQ's pricing waterfall, helping you understand how different elements impact the final Net Price. As you enter values, the calculator shows how discounts work together, just like in CPQ, giving you a clear picture of how adjustments affect pricing at each stage.
date: 2024-06-20 10:00:00 +0300
author: admin
image: /images/pricingWaterfall.png
hide_image: true
image_caption:
tags: [tools, legacy-cpq]
featured:
video_embed:
permalink: /cpq-price-waterfall-calculator/
---

<style>
    #output {
        font-weight: 1000;
    }

    .calculator-container {
        margin: auto;
        padding: 20px;
        background-color: white;
        box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
        border-radius: 8px;
    }

    form {
        display: flex;
        flex-direction: column;
    }

    ol {
        list-style-type: decimal;
        padding-left: 20px;
    }

    li {
        margin-bottom: 15px;
    }

    label {
        margin: 10px 0 5px;
        color: #555;
        font-weight: 600;
        display: block;
    }

    input {
        padding: 10px;
        border-radius: 4px;
        border: 1px solid #ccc;
        font-size: 16px;
        box-sizing: border-box;
        width: 95%;
    }

    button {
        padding: 10px;
        background-color: #007BFF;
        color: white;
        border: none;
        border-radius: 4px;
        font-size: 16px;
        cursor: pointer;
        transition: background-color 0.3s ease;
    }

    button:hover {
        background-color: #0056b3;
    }

    input[readonly] {
        background-color: #e9ecef;
        cursor: not-allowed;
    }

    .info-icon {
        font-size: 12px;
        position: relative;
        top: -8px;
        vertical-align: middle;
    }

    .net-price-card {
        margin: 0px 0 0 0;
        margin-left: 18px;
        padding: 20px;
        background-color: #f8f9fa;
        border: 1px solid #ddd;
        border-radius: 8px;
        box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
        text-align: center;
        width: 95%;
    }

    .net-price-card h3 {
        margin-bottom: 15px;
        font-size: 18px;
        font-weight: 700;
        color: #333;
    }

    .net-price-card input {
        font-size: 20px;
        font-weight: bold;
        color: #03b800;
        text-align: center;
        width: 100%;
    }

    #fork-me-container {
        margin-top: 15px;
        text-align: center;
    }

    #fork-me {
        display: inline-flex;
        align-items: center;
        justify-content: center;
    }

</style>


<div class="calculator-container">
    <form id="priceForm">
        <ol>
            <!-- List Price -->
            <li>
                <label for="listPrice">List Price
                    <span class="info-icon" title="Price pulled from the quote's associated Price Book" style="cursor: pointer;">&#9432;</span>
                </label>
                <input type="number" id="listPrice" name="listPrice" step="0.01" placeholder="Start Here" onblur="calculatePrices(this.id)">
            </li>

            <!-- Contracted Price -->
            <li>
                <label for="contractedPrice" class="optional">Contracted Price
                    <span class="info-icon" title="Price contracted for Account on Quote" style="cursor: pointer;">&#9432;</span>
                </label>
                <input type="number" id="contractedPrice" name="contractedPrice" step="0.01" onblur="calculatePrices(this.id)">
            </li>

            <!-- Special Price -->
            <li>
                <label for="specialPrice" class="optional">Special Price
                    <span class="info-icon" title="Special unit price for this line item, such as volume discount or contracted price" style="cursor: pointer;">&#9432;</span>
                </label>
                <input type="number" id="specialPrice" name="specialPrice" step="0.01" onblur="calculatePrices(this.id)">
            </li>

            <!-- Prorate Multiplier -->
            <li>
                <label for="prorateMultiplier">Prorate Multiplier
                    <span class="info-icon" title="Controlled by CPQ Package Settings" style="cursor: pointer;">&#9432;</span>
                </label>
                <input type="number" id="prorateMultiplier" name="prorateMultiplier" step="0.01" value="1" onblur="calculatePrices(this.id)">
            </li>

            <!-- Prorated Price -->
            <li>
                <label for="proratedPrice">Prorated Price</label>
                <input type="number" id="proratedPrice" name="proratedPrice" step="0.01" readonly>
            </li>

            <!-- Regular Price -->
            <li>
                <label for="regularPrice">Regular Price
                    <span class="info-icon" title="Prorated list price after system discounts or the Special Price if a Special Price Type is specified" style="cursor: pointer;">&#9432;</span>
                </label>
                <input type="number" id="regularPrice" name="regularPrice" step="0.01" onblur="calculatePrices(this.id)">
            </li>

            <!-- Additional Discount Percent -->
            <li>
                <label for="additionalDiscountPercent">Additional Discount
                    <span class="info-icon" title="Value entered by sales users or pricing guidance" style="cursor: pointer;">&#9432;</span>
                </label>
                <input type="number" id="additionalDiscountPercent" name="additionalDiscountPercent" step="0.01" placeholder="%" onblur="calculatePrices(this.id)">
            </li>

            <!-- Customer Price -->
            <li>
                <label for="customerPrice">Customer Price
                    <span class="info-icon" title="Regular Price minus Additional Discount" style="cursor: pointer;">&#9432;</span>
                </label>
                <input type="number" id="customerPrice" name="customerPrice" step="0.01" onblur="calculatePrices(this.id)">
            </li>

            <!-- Partner Discount Percent -->
            <li>
                <label for="partnerDiscountPercent" class="optional">Partner Discount
                    <span class="info-icon" title="Discount given to selling partner, entered by the sales user" style="cursor: pointer;">&#9432;</span>
                </label>
                <input type="number" id="partnerDiscountPercent" name="partnerDiscountPercent" step="0.01" placeholder="%" onblur="calculatePrices(this.id)">
            </li>

            <!-- Partner Price -->
            <li>
                <label for="partnerPrice">Partner Price
                    <span class="info-icon" title="Customer Price minus Partner Discount" style="cursor: pointer;">&#9432;</span>
                </label>
                <input type="number" id="partnerPrice" name="partnerPrice" step="0.01" onblur="calculatePrices(this.id)">
            </li>

            <!-- Distributor Discount Percent -->
            <li>
                <label for="distributorDiscountPercent" class="optional">Distributor Discount
                    <span class="info-icon" title="Discount given to distributor, entered by sales user" style="cursor: pointer;">&#9432;</span>
                </label>
                <input type="number" id="distributorDiscountPercent" name="distributorDiscountPercent" step="0.01" placeholder="%" onblur="calculatePrices(this.id)">
            </li>
        </ol>

        <!-- Net Price Card -->
        <div class="net-price-card">
            <h3>Net Price</h3>
            <input type="number" id="netPrice" name="netPrice" step="0.01" readonly>
        </div>
    </form>


</div>
<br>
<!-- <div id="fork-me-container">
    <a href="https://github.com/sr7d/cpq-pricing-water-simulator/fork" target="_blank">
        <button class="button button--primary" id="fork-me">
            <i class="ion ion-logo-github" style="margin-right: 5px;"></i>
            Fork Me on Github
        </button>
    </a>
</div> -->



<script>
    function calculatePrices(changedFieldId) {
        console.log('Changed Field ID:', changedFieldId);

/*===================
Calculation Rank
====================*/
        function calculateRank(changedFieldId) {
            let rank;
            switch (changedFieldId) {
                case 'listPrice':
                    rank = 1;
                    break;
                case 'contractedPrice':
                    rank = 2;
                    break;
                case 'specialPrice':
                    rank = 3;
                    break;
                case 'prorateMultiplier':
                    rank = 4;
                    break;
                case 'proratedPrice':
                    rank = 5;
                    break;
                case 'regularPrice':
                    rank = 6;
                    break;
                case 'additionalDiscountPercent':
                    rank = 7;
                    break;
                case 'customerPrice':
                    rank = 8;
                    break;
                case 'partnerDiscountPercent':
                    rank = 9;
                    break;
                case 'partnerPrice':
                    rank = 10;
                    break;
                case 'distributorDiscountPercent':
                    rank = 11;
                    break;
                default:
                    rank = null;
            }
            return rank;
        }

        let calculationRank = calculateRank(changedFieldId);
        console.log('Calculation Rank:', calculationRank);

/*===================
Default Values
====================*/
        let listPrice;
        let contractedPrice;

        let specialPrice = document.getElementById('specialPrice').value;
        document.getElementById('specialPrice').style.color = 'fieldtext';

        let prorateMultiplier = 1;
        document.getElementById('prorateMultiplier').style.color = 'fieldtext';

        let proratedPrice = document.getElementById('proratedPrice').value;
        document.getElementById('proratedPrice').style.color = 'fieldtext';

        let regularPrice = document.getElementById('regularPrice').value;
        document.getElementById('regularPrice').style.color = 'fieldtext';

        let additionalDiscountPercent = document.getElementById('additionalDiscountPercent').value;
        document.getElementById('additionalDiscountPercent').style.color = 'fieldtext';

        let customerPrice = document.getElementById('customerPrice').value;
        document.getElementById('customerPrice').style.color = 'fieldtext';

        let partnerDiscountPercent = document.getElementById('partnerDiscountPercent').value;
        document.getElementById('partnerDiscountPercent').style.color = 'fieldtext';

        let partnerPrice = document.getElementById('partnerPrice').value;
        document.getElementById('partnerPrice').style.color = 'fieldtext';

        let netPrice = 0;

/*===================
On List Price Change
====================*/
if (calculationRank === 1) {
            listPrice = parseFloat(document.getElementById('listPrice').value) || 0;
            document.getElementById('listPrice').value = listPrice.toFixed(2);

            specialPrice = listPrice;
            document.getElementById('specialPrice').value = specialPrice.toFixed(2);
            document.getElementById('specialPrice').style.color = 'orange';

            proratedPrice = prorateMultiplier * specialPrice;
            document.getElementById('proratedPrice').value = proratedPrice.toFixed(2);
            document.getElementById('proratedPrice').style.color = 'orange';

            regularPrice = proratedPrice;
            document.getElementById('regularPrice').value = regularPrice.toFixed(2);
            document.getElementById('regularPrice').style.color = 'orange';

            customerPrice = regularPrice;
            document.getElementById('customerPrice').value = customerPrice.toFixed(2);
            document.getElementById('customerPrice').style.color = 'orange';

            partnerPrice = customerPrice;
            document.getElementById('partnerPrice').value = partnerPrice.toFixed(2);
            document.getElementById('partnerPrice').style.color = 'orange';

            netPrice = partnerPrice;
            document.getElementById('netPrice').value = netPrice.toFixed(2);

        }

/*===================
On Contracted Price Change
====================*/
if (calculationRank === 2) {
    contractedPrice = parseFloat(document.getElementById('contractedPrice').value) || 0;
    document.getElementById('contractedPrice').value = contractedPrice.toFixed(2);

    specialPrice = contractedPrice;
    document.getElementById('specialPrice').value = specialPrice.toFixed(2);
    document.getElementById('specialPrice').style.color = 'orange';

    proratedPrice = prorateMultiplier * specialPrice;
    document.getElementById('proratedPrice').value = proratedPrice.toFixed(2);
    document.getElementById('proratedPrice').style.color = 'orange';

    regularPrice = proratedPrice;
    document.getElementById('regularPrice').value = regularPrice.toFixed(2);
    document.getElementById('regularPrice').style.color = 'orange';

    customerPrice = regularPrice;
    document.getElementById('customerPrice').value = customerPrice.toFixed(2);
    document.getElementById('customerPrice').style.color = 'orange';

    partnerPrice = customerPrice;
    document.getElementById('partnerPrice').value = partnerPrice.toFixed(2);
    document.getElementById('partnerPrice').style.color = 'orange';

    netPrice = partnerPrice;
    document.getElementById('netPrice').value = netPrice.toFixed(2);

}

/*===================
On Special Price Change
====================*/
if (calculationRank === 3) {
    specialPrice = parseFloat(document.getElementById('specialPrice').value) || 0;
    document.getElementById('specialPrice').value = specialPrice.toFixed(2);

    proratedPrice = prorateMultiplier * specialPrice;
    document.getElementById('proratedPrice').value = proratedPrice.toFixed(2);
    document.getElementById('proratedPrice').style.color = 'orange';

    regularPrice = proratedPrice;
    document.getElementById('regularPrice').value = regularPrice.toFixed(2);
    document.getElementById('regularPrice').style.color = 'orange';

    customerPrice = regularPrice;
    document.getElementById('customerPrice').value = customerPrice.toFixed(2);
    document.getElementById('customerPrice').style.color = 'orange';

    partnerPrice = customerPrice;
    document.getElementById('partnerPrice').value = partnerPrice.toFixed(2);
    document.getElementById('partnerPrice').style.color = 'orange';

    netPrice = partnerPrice;
    document.getElementById('netPrice').value = netPrice.toFixed(2);

}

/*===================
On Prorate Multiplier Change
====================*/
if (calculationRank === 4) {
    prorateMultiplier = parseFloat(document.getElementById('prorateMultiplier').value);
    document.getElementById('prorateMultiplier').value = prorateMultiplier.toFixed(2);

    proratedPrice = prorateMultiplier * specialPrice;
    document.getElementById('proratedPrice').value = proratedPrice.toFixed(2);
    document.getElementById('proratedPrice').style.color = 'orange';

    regularPrice = proratedPrice;
    document.getElementById('regularPrice').value = regularPrice.toFixed(2);
    document.getElementById('regularPrice').style.color = 'orange';

    customerPrice = regularPrice;
    document.getElementById('customerPrice').value = customerPrice.toFixed(2);
    document.getElementById('customerPrice').style.color = 'orange';

    partnerPrice = customerPrice;
    document.getElementById('partnerPrice').value = partnerPrice.toFixed(2);
    document.getElementById('partnerPrice').style.color = 'orange';

    netPrice = partnerPrice;
    document.getElementById('netPrice').value = netPrice.toFixed(2);

}
/*===================
On Regular Price Change
====================*/
if (calculationRank === 6) {
    regularPrice = parseFloat(document.getElementById('regularPrice').value);
    document.getElementById('regularPrice').value = regularPrice.toFixed(2);

    customerPrice = regularPrice;
    document.getElementById('customerPrice').value = customerPrice.toFixed(2);
    document.getElementById('customerPrice').style.color = 'orange';

    partnerPrice = customerPrice;
    document.getElementById('partnerPrice').value = partnerPrice.toFixed(2);
    document.getElementById('partnerPrice').style.color = 'orange';

    netPrice = partnerPrice;
    document.getElementById('netPrice').value = netPrice.toFixed(2);

}

/*===================
On Additional Discount Change
====================*/
if (calculationRank === 7) {
    additionalDiscountPercent = parseFloat(document.getElementById('additionalDiscountPercent').value);
    document.getElementById('additionalDiscountPercent').value = additionalDiscountPercent.toFixed(2);

    customerPrice = regularPrice * (1 - additionalDiscountPercent / 100);
    document.getElementById('customerPrice').value = customerPrice.toFixed(2);
    document.getElementById('customerPrice').style.color = 'orange';

    partnerPrice = customerPrice;
    document.getElementById('partnerPrice').value = partnerPrice.toFixed(2);
    document.getElementById('partnerPrice').style.color = 'orange';

    netPrice = partnerPrice;
    document.getElementById('netPrice').value = netPrice.toFixed(2);

}

/*===================
On Customer Price Change
====================*/
if (calculationRank === 8) {
    customerPrice = parseFloat(document.getElementById('customerPrice').value);
    document.getElementById('customerPrice').value = customerPrice.toFixed(2);

    partnerPrice = customerPrice;
    document.getElementById('partnerPrice').value = partnerPrice.toFixed(2);
    document.getElementById('partnerPrice').style.color = 'orange';

    netPrice = partnerPrice;
    document.getElementById('netPrice').value = netPrice.toFixed(2);

}

/*===================
On Partner Discount Change
====================*/
if (calculationRank === 9) {
    partnerDiscountPercent = parseFloat(document.getElementById('partnerDiscountPercent').value) || 0;
    document.getElementById('partnerDiscountPercent').value = partnerDiscountPercent.toFixed(2);

    partnerPrice = customerPrice * (1 - partnerDiscountPercent / 100);
    document.getElementById('partnerPrice').value = partnerPrice.toFixed(2);
    document.getElementById('partnerPrice').style.color = 'orange';

    netPrice = partnerPrice;
    document.getElementById('netPrice').value = netPrice.toFixed(2);
}


/*===================
On Partner Price Change
====================*/
if (calculationRank === 10) {
    partnerPrice = parseFloat(document.getElementById('partnerPrice').value) || 0;
    document.getElementById('partnerPrice').value = partnerPrice.toFixed(2);
    document.getElementById('partnerPrice').style.color = 'orange';

    netPrice = partnerPrice;
    document.getElementById('netPrice').value = netPrice.toFixed(2);
}

/*===================
On Distributor Discount Change
====================*/
if (calculationRank === 11) {
    distributorDiscountPercent = parseFloat(document.getElementById('distributorDiscountPercent').value);
    netPrice = partnerPrice * (1 - distributorDiscountPercent / 100);
    document.getElementById('netPrice').value = netPrice.toFixed(2);
}

    }

</script>
