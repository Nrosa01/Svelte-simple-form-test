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

    let div;
    let button;

    // Functions to move the button
    
    let getDivWidth = () => parseInt(window.getComputedStyle(div, null).width)
    let getButtonWidth = () => parseInt(window.getComputedStyle(button, null).width)
    
    let pixelsToPercentage = (pixels) => (pixels / getDivWidth()) * 100;
    let correctPosition = (threshold) => Math.abs(newPos - currentPos) >= threshold;
    let findNewPosition = () => newPos = Math.floor(Math.random() * 100) - 50;
    let clampPosition = () =>
    {
        let maxRight = pixelsToPercentage( getDivWidth()/2  - (getButtonWidth()/2))
        let maxLeft = pixelsToPercentage(- getDivWidth()/2 + (getButtonWidth()/2))

        newPos = Math.min(Math.max(newPos, maxLeft), maxRight);
    }
    
    // Listener to move the button on windows resize
    window.addEventListener('resize', function(event) {
        onResize();
    }, true);


    function move()
    {
        if(!funnyMode)
            return;

        // Save last pos
        currentPos = newPos;

        let counter = 100;
        do
        {
            findNewPosition();
            clampPosition();
            counter--;
        } while(!correctPosition(25) && counter > 0)
    }

    function onResize()
    {
        clampPosition();
    }

    function onFocus()
    {
        if(!canBeClicked)
        if (document.activeElement instanceof HTMLElement)
            document.activeElement.blur();
    }
</script>

<div bind:this="{div}" class="flex justify-center">
    <button bind:this="{button}" class="{classes}"
    style='transition: left 0.25s ease-in-out; left: {canBeClicked ? 0 : newPos}%;'
    type="button" on:click on:mouseenter="{() => move()}" on:focus="{() => onFocus()}">
    <slot></slot>
</button>
</div>