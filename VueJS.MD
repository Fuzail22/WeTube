<h1 align="center"> VUE JS </h1>
<p align="center"> Get to know about VUE building the platform</p>

## VUE Lifcycle:
1. Creation Phase:
### functions present: 
beforeCreate: Called synchronously after the instance has just been initialized.
created: Called synchronously after the instance has been created.

2. Mounting Phase:
### functions present: 
beforeMount: Called right before the component is mounted to the DOM.
mounted: Called after the component has been mounted to the DOM.

3. Updating Phase:
### functions present: 
beforeUpdate: Called when the data changes, just before the virtual DOM and DOM are patched.
updated: Called after the data changes and the virtual DOM and DOM have been patched.

4. Destruction Phase:
### functions present: 
beforeDestroy: Called right before the instance is destroyed.
destroyed: Called after the instance is destroyed.

## VUE Basics
1. refractive vs ref
2. The **watch** option in a Vue is used to observe changes to a specific property and execute a function when that property changes. 
    ```
    watch: {
        videoUrl() {
          this.handleFileChange();
        },
      }
    ```
    >In the above example, the watch option is being used to monitor changes to the videoUrl property and trigger the
    >handleFileChange method whenever videoUrl changes.
3. The **created()** function is called during the Creation Phase as mentioned aboved in the lifecycle.
    ```
    created() {
    eventBus.$on("update-subtitles-url", (newUrl) => {
      this.subtitlesUrl = newUrl;
    });
    >in the above example,  the created function was used to set up an event listener (eventBus.$on) within the
    >VideoPlayerComponent. This event listener would start listening for the "update-subtitles-url" event as soon as the         >component is created.
