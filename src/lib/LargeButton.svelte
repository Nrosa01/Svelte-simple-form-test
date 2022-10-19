<script>
    export let canBeClicked = false;

    let funnyMode = true;
    let currentPos = 0;
    let newPos = 0;
    let buttonClassBase = "relative w-full:funnyMode px-6 py-2 mt-4 text-white rounded-lg hover:bg-blue-900";
    let canClickButtonClass = "bg-green-600"
    let cantClickButtonClass = "bg-blue-600"
    let funnyModeClass = `${!funnyMode ? "w-full" : ""}`

    $: classes = `${buttonClassBase} ${canBeClicked ? canClickButtonClass : cantClickButtonClass} ${funnyModeClass}`

    function move()
    {
        if(!funnyMode)
            return;

        let button = document.getElementById("button");
        let cssButton = window.getComputedStyle(button, null);
        let div = document.getElementById("div");
        let cssDiv = window.getComputedStyle(div, null);

        currentPos = newPos;
        //newpos must bet -50 50
        newPos = Math.floor(Math.random() * 100) - 50;

        while (Math.abs(newPos - currentPos) < 25)
            newPos = Math.floor(Math.random() * 100) - 50;

        if(canBeClicked)
            newPos = 0;

        let buttonWidth = parseInt(cssButton.width);     
        let divWidth = parseInt(cssDiv.width);

        //lambda function to convert pixels to percentage
        let pixelsToPercentage = (pixels) => (pixels / divWidth) * 100;
        let percentageToPixels = (percentage) => (percentage / 100) * divWidth;

        let maxRight = pixelsToPercentage(divWidth/2  - (buttonWidth/2))
        let maxLeft = pixelsToPercentage(-divWidth/2 + (buttonWidth/2))

        //Clamp newpos between maxRight and maxLeft
        newPos = Math.min(Math.max(newPos, maxLeft), maxRight);
        button.style.left = `${newPos}%`;
    }

    function onFocus()
    {
        if(!canBeClicked)
        if (document.activeElement instanceof HTMLElement)
            document.activeElement.blur();
    }
</script>

<div id="div" class="flex justify-center">
    <button id="button" class="{classes}"
    style='transition: left 0.25s ease-in-out; left: {canBeClicked ? 0 : newPos}%;'
    type="button" on:click on:mouseenter="{() => move()}" on:focus="{() => onFocus()}">
    <slot></slot>
</button>
</div>