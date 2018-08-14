<template>
  <section>
    <h1>hp</h1>
    <!-- <div class="image"></div> -->
    <div class="image">
      <img class="image" src="image.jpg" alt="test">
    </div>
  </section>
</template>

<style>
.image {
  position: relative;
}

.part {
  position: absolute;
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background-color: red;
}
</style>


<script>
import * as posenet from '@tensorflow-models/posenet'

export default {
  mounted () {
    var imageScaleFactor = 0.5;
    var flipHorizontal = false;
    var outputStride = 16;
    var maxPoseDetections = 2;

    // function loadImage(url) {
    //   return new Promise((resolve, reject) => {
    //     let img = new Image();
    //     img.addEventListener('load', e => resolve(img));
    //     img.addEventListener('error', () => {
    //       reject(new Error(`Failed to load image's URL: ${url}`));
    //     });
    //     img.src = url;
    //   });
    // }

    // // load the image, and append it to the element id="image-holder"
    // loadImage('https://loremflickr.com/1200/640/federer')
    //   .then(function (img) {
    //     document.querySelector('.image').appendChild(img)

    //     console.log(img)

    //     posenet.load().then(function(net) {
    //       return net.estimateMultiplePoses(img, 0.5, flipHorizontal, outputStride, maxPoseDetections)
    //     }).then(function(poses){
    //       console.log(poses);

    //       for (let i = 0; i < poses.length; i++) {
    //         const el = poses[i];
    //         console.log(el.keypoints)

    //         for (let k = 0; k < el.keypoints.length; k++) {
    //           const childEl = el.keypoints[k];
    //           console.log(childEl)

    //           let part = document.createElement('div')
    //           part.className = 'part '
    //           part.className += childEl.part

    //           part.style.top = parseInt(childEl.position.y) + 'px'
    //           part.style.left = parseInt(childEl.position.x) + 'px'

    //           console.log(part)

    //           document.querySelector('section').appendChild(part)
    //         }
    //       }
    //     })
    //   })
    //   .catch(error => console.error(error));

    posenet.load().then(function(net) {
        return net.estimateMultiplePoses(document.querySelector('.image img'), 0.5, flipHorizontal, outputStride, maxPoseDetections)
      }).then(function(poses){
        console.log(poses);

        for (let i = 0; i < poses.length; i++) {
          const el = poses[i];
          console.log(el.keypoints)

          for (let k = 0; k < el.keypoints.length; k++) {
            const childEl = el.keypoints[k];
            console.log(childEl)

            let part = document.createElement('div')
            part.className = 'part '
            part.className += childEl.part

            part.style.top = parseInt(childEl.position.y) + 'px'
            part.style.left = parseInt(childEl.position.x) + 'px'

            console.log(part)

            document.querySelector('section').appendChild(part)
          }
        }
      })
  }
}
</script>