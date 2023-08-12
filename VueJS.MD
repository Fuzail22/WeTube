<h1 align="center"> VUE JS </h1>
<p align="center"> Get to know about VUE building the platform</p>

## VUE Basics
1. refractive vs ref
2. The watch option in a Vue is used to observe changes to a specific property and execute a function when that property changes. 
    ```
    watch: {
        videoUrl() {
          this.handleFileChange();
        },
      },
    ```
    >In the above example the watch option is being used to monitor changes to the videoUrl property and trigger the
    >handleFileChange method whenever videoUrl changes.
