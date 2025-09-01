---
date: '2025-08-29T11:53:04-07:00'
draft: true
title: 'Fancy Restaurant Menu'
---

#### Let's Eat

Pâté of roasted indigenous legumes, paired with a compote of seasonal berries?, Anyone?

I live in Camas Washington, a suburb of Vancouver WA, which in itself would be considered a suburb or Portland OR, Camas is beautiful indeed, and wouldn't live anywhere else, but Camas is not Bordeaux, or Dijon, yet some restaurants seem to disagree with me.

I would not consider myself cheap per se, but when you start seeing words like "_Deconstructed_", "_Foraged_", "_Aioli_", "_fresh cracked pepper_", "_buttermilk-soaked_", etc. - On an otherwise quaint little town's downtown restaurants, then you get the picture.. it becomes a bit annoying.

Take for example, this _Menu item_:

**Pâté of roasted indigenous legumes, paired with a compote of seasonal berries, served on hearty sprouted wheat bread.**

You realize that the above just means <mark>Peanut Butter and Jelly Sandwich</mark>.

So why the pompous name then, well, a PBJS will set you back, say 3 bucks, whereas our hearty wheat bread option can ring up to 6, or 7 dollars a piece, a nice 100%+ markup for fancy words, _sacré Bleu_!!.

Up-selling in the restaurant industry is a huge industry in and on itself, and apparently it works, it just doesn't for me.

So in the spirit of giving to all folkspeople like me a gift, I present you with with my amazing "Fancy Menu Generator", so if/when you decide to open your own restaurant in downtown, get your menu ready, and slap on it an outrageous price on the items (suggested price included), you can't go wrong, here it is:

#### Show me the menu

<a href="javascript:void(0)" title="Generate Menu" onclick="return FancyMenu.show();">Generate New Menu</a> |
<a href="javascript:void(0)" title="Clear Menu" onclick="return FancyMenu.clear();">Clear Menu</a>

<div id="fancy-menu" style="margin:10px 0;"></div>

#### Da Code

Code was implemented as an IIFE for simplicity, it is pure Javascript without any external dependencies, all you
need to do is create a `<div id="fancy-menu"></div>` _wrapper_ html element and call it from a link or button with
a similar structure:

```html
<a href="javascript:void(0)" title="Generate Menu" onclick="FancyMenu.show();">Generate Menu</a>
```

```javascript
let FancyMenu = (() => {
    let _generate = {},
        show,
        clear,
        getPriceInt,
        chooseOneOf,
        nouns = [
            'Infusion', 'Suggestion', 'Memory', 'Whisper', 'Cloud',
            'Distillation', 'Essence', 'Deconstruction', 'Cream',
            'Suppression', 'Ragu', 'Purée', 'Foam', 'Blade',
            'Carpaccio', 'Dumpling', 'Velouté', 'Raviolli',
            'Compote', 'Emulsion',
            'Palette', 'Curd', 'Bricolage', 'Casserole'],
        cook_method = [
            'Water-Bathed', 'Broiled', 'Flame-Roasted',
            'Blackened', 'Braised', 'fondant', 'Liquidised',
            'Nitro-Poached', 'Jellied', 'Hand-Carved',
            'Shaved', 'Josper-Baked', 'Kiln-Smoked', 'Hashed',
            'Salt-Crusted', 'Macerated', 'Flattened', 'Bain-marie',
            'Ionized', 'Pickled', 'Maple-Cured'],
        trendy = [
            'Woodcock', 'Sea Scallops', 'Calf\'s Liver',
            'John Dory', 'Sweetbread', 'Langoustines',
            'Black Pudding', 'Squab Pigeon', 'Monkfish',
            'Aĩoli Hancock', 'Black Bream', 'Chorizo', 'Quail',
            'Barramundi', 'Octopus', 'Bone Marrow', 'Duck Breast',
            'Pig\'s Trotter', 'Sea Bass', 'Serrano Ham'],
        serve_method = [
            'floated', 'draped', 'bubbled',
            'reasting', 'heaped', 'layered',
            'combined ', 'served', 'entwined',
            'on a bed', 'spliced', 'tossed',
            'plated with', 'enrobed by', 'accompanied',
            'injected', 'presented', 'laced',
            'arranged', 'nested', 'Chiffonade'],
        prepositions = ['on', 'over', 'with', 'in', 'by', 'through', 'within'],
        upsale = [
            'unique', 'hand', 'locally-sourced', 'perennial',
            'chef\'s choice', 'decomposed', '', 'triple-basted',
            'seasonal', 'arabesque', 'spanish', 'mediterranean',
            'locally-inspired', 'hollistically assembled',
            'a dash of', 'slow roasted'],
        prep_method = [
            'Mashed', 'Diced', 'Sliced', 'Cubed', 'Pan-Fried',
            'Crushed', 'Provenčal', 'Wafered', 'Sauteed',
            'Artisan', 'Slop-Poached', 'Responsibly Sourced',
            'Griddled', 'Marinated', 'Boiled', 'Aromatic',
            'Buttered', 'Two-Way', 'Herbed', 'Heritage'],
        side = [
            'Baby Turnips', 'Cabbage', 'Potato', 'Tomato Bed', 'Chervil',
            'Aubergine', 'Courgette', 'Beetroot', 'Spring Onion',
            'Radishes', 'Asparragus', 'Black Olives', 'Celeriac',
            'Herbs de Provence',
            'Purple Sprouting Broccoli', 'Chard', 'Chicory',
            'Semphire', 'Mung Beans', 'Fennel', 'Watercress'];

    chooseOneOf = (arrSize) => {
        return Math.floor(Math.random() * arrSize);
    };

    _generate = (numItems) => {
        numItems = typeof (numItems) === 'number' ? numItems : 5;
        let items = [];
        for (let i = 0; i < numItems; i++) {
            items.push(
                nouns[chooseOneOf(nouns.length)] +
                ' of ' +
                cook_method[chooseOneOf(cook_method.length)] + ' ' +
                trendy[chooseOneOf(trendy.length)] + ' ' +
                serve_method[chooseOneOf(serve_method.length)] + ' ' +
                prepositions[chooseOneOf(prepositions.length)] + ' ' +
                upsale[chooseOneOf(upsale.length)] + ' ' +
                prep_method[chooseOneOf(prep_method.length)] + ' ' +
                side[chooseOneOf(side.length)] + ', $' +
                getPriceInt().toString() + '.95');
        }
        return items;
    };

    show = (menuItems) => {
        clear();
        let items = _generate(typeof menuItems === 'number' ? menuItems : 10);
        let fancyMenuContainer = document.getElementById('fancy-menu');
        fancyMenuContainer.insertAdjacentHTML('beforeend', '<ol>');
        items.forEach(function (item) {
            fancyMenuContainer.insertAdjacentHTML('beforeend', '<li>' + item + '</li>');
        });
        fancyMenuContainer.insertAdjacentHTML('beforeend', '</ol>');
    };

    clear = () => {
        document.getElementById('fancy-menu').innerHTML = '';
    };

    getPriceInt = () => {
        /* Returns a value for a fancy menu item */
        let min = Math.ceil(17),
            max = Math.floor(26);
        return Math.floor(Math.random() * (max - min) + min);
    }

    return {
        show: show,
        clear: clear
    };
})();
```

<script data-isso="//isso.rustix.dev/" src="//isso.rustix.dev/js/embed.min.js"></script>
<section id="isso-thread">
    <noscript>Javascript needs to be activated to view comments.</noscript>
</section>

<script>
let FancyMenu = (() => {
    let _generate = {},
        show,
        clear,
        getPriceInt,
        chooseOneOf,
        nouns = [
            'Infusion', 'Suggestion', 'Memory', 'Whisper', 'Cloud',
            'Distillation', 'Essence', 'Deconstruction', 'Cream',
            'Suppression', 'Ragu', 'Purée', 'Foam', 'Blade',
            'Carpaccio', 'Dumpling', 'Velouté', 'Raviolli',
            'Compote', 'Emulsion',
            'Palette', 'Curd', 'Bricolage', 'Casserole'],
        cook_method = [
            'Water-Bathed', 'Broiled', 'Flame-Roasted',
            'Blackened', 'Braised', 'fondant', 'Liquidised',
            'Nitro-Poached', 'Jellied', 'Hand-Carved',
            'Shaved', 'Josper-Baked', 'Kiln-Smoked', 'Hashed',
            'Salt-Crusted', 'Macerated', 'Flattened', 'Bain-marie',
            'Ionized', 'Pickled', 'Maple-Cured'],
        trendy = [
            'Woodcock', 'Sea Scallops', 'Calf\'s Liver',
            'John Dory', 'Sweetbread', 'Langoustines',
            'Black Pudding', 'Squab Pigeon', 'Monkfish',
            'Aĩoli Hancock', 'Black Bream', 'Chorizo', 'Quail',
            'Barramundi', 'Octopus', 'Bone Marrow', 'Duck Breast',
            'Pig\'s Trotter', 'Sea Bass', 'Serrano Ham'],
        serve_method = [
            'floated', 'draped', 'bubbled',
            'reasting', 'heaped', 'layered',
            'combined ', 'served', 'entwined',
            'on a bed', 'spliced', 'tossed',
            'plated with', 'enrobed by', 'accompanied',
            'injected', 'presented', 'laced',
            'arranged', 'nested', 'Chiffonade'],
        prepositions = ['on', 'over', 'with', 'in', 'by', 'through', 'within'],
        upsale = [
            'unique', 'hand', 'locally-sourced', 'perennial',
            'chef\'s choice', 'decomposed', '', 'triple-basted',
            'seasonal', 'arabesque', 'spanish', 'mediterranean',
            'locally-inspired', 'hollistically assembled',
            'a dash of', 'slow roasted'],
        prep_method = [
            'Mashed', 'Diced', 'Sliced', 'Cubed', 'Pan-Fried',
            'Crushed', 'Provenčal', 'Wafered', 'Sauteed',
            'Artisan', 'Slop-Poached', 'Responsibly Sourced',
            'Griddled', 'Marinated', 'Boiled', 'Aromatic',
            'Buttered', 'Two-Way', 'Herbed', 'Heritage'],
        side = [
            'Baby Turnips', 'Cabbage', 'Potato', 'Tomato Bed', 'Chervil',
            'Aubergine', 'Courgette', 'Beetroot', 'Spring Onion',
            'Radishes', 'Asparragus', 'Black Olives', 'Celeriac',
            'Herbs de Provence',
            'Purple Sprouting Broccoli', 'Chard', 'Chicory',
            'Semphire', 'Mung Beans', 'Fennel', 'Watercress'];

    chooseOneOf = (arrSize) => {
        return Math.floor(Math.random() * arrSize);
    };

    _generate = (numItems) => {
        numItems = typeof (numItems) === 'number' ? numItems : 5;
        let items = [];
        for (let i = 0; i < numItems; i++) {
            items.push(
                nouns[chooseOneOf(nouns.length)] +
                ' of ' +
                cook_method[chooseOneOf(cook_method.length)] + ' ' +
                trendy[chooseOneOf(trendy.length)] + ' ' +
                serve_method[chooseOneOf(serve_method.length)] + ' ' +
                prepositions[chooseOneOf(prepositions.length)] + ' ' +
                upsale[chooseOneOf(upsale.length)] + ' ' +
                prep_method[chooseOneOf(prep_method.length)] + ' ' +
                side[chooseOneOf(side.length)] + ', $' +
                getPriceInt().toString() + '.95');
        }
        return items;
    };

    show = (menuItems) => {
        clear();
        let items = _generate(typeof menuItems === 'number' ? menuItems : 10);
        let fancyMenuContainer = document.getElementById('fancy-menu');
        fancyMenuContainer.insertAdjacentHTML('beforeend', '<ol>');
        items.forEach(function (item) {
            fancyMenuContainer.insertAdjacentHTML('beforeend', '<li>' + item + '</li>');
        });
        fancyMenuContainer.insertAdjacentHTML('beforeend', '</ol>');
    };

    clear = () => {
        document.getElementById('fancy-menu').innerHTML = '';
    };

    getPriceInt = () => {
        /* Returns a value for a fancy menu item */
        let min = Math.ceil(17),
            max = Math.floor(26);
        return Math.floor(Math.random() * (max - min) + min);
    }

    return {
        show: show,
        clear: clear
    };
})();
FancyMenu.show();
</script>
