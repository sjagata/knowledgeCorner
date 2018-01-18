### Image scaling based on parent div

```js
            var dropzoneEle = dropzone.element;
            var eleID = dropzoneEle.id;
            var element = $('#' + eleID + ' .dz-image').last().find('img')[0];
            var $parent = $(element).parent();
            var valueAccessor = {
                width: 175,
                height: null
            };

            window.console.warn("dropzone", dropzone, element, eleID);

            var containerWidth = valueAccessor.width || $parent[0].clientWidth;
            var containerHeight = valueAccessor.height || $parent[0].clientHeight;

            var scaleX = containerWidth / file.width;
            var scaleY = containerHeight / file.height;

            var scaleRatio = Math.min(scaleX, scaleY);
            var width = Math.round(file.width * scaleRatio);
            var height = Math.round(file.height * scaleRatio);

            $(element).addClass(scaleX < scaleY ? "bf-img-wider" : "bf-img-longer");

            if (width) {
                dropzone.options.thumbnailWidth = width;
                dropzone.options.thumbnailHeight = height;
                element.style.setProperty('width', width + 'px', 'important');
                element.style.setProperty('height', height + 'px', 'important');
            } else {
                window.console.warn("could not determine width and height for image");
                window.console.warn("image", element.naturalWidth, element.naturalHeight, containerWidth, containerHeight, scaleX, scaleY);
                window.console.warn("scale", width, height, scaleRatio);
            }
            ```
