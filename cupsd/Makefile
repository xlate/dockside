.RECIPEPREFIX +=

image:
    docker build -t xlate/cupsd .

container:
    docker run -dit --rm --name cupsd -p 1631:631 xlate/cupsd

execbash:
    docker exec -it cupsd /bin/bash

clean:
    docker kill cupsd
