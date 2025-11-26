## Image is created in layers
***Test:*** DOCKER_BUILDKIT=0 docker build --progress=plain -t chakradhar05/catalogue:v1 .
- Docker creates container for FROM instruction.
- Runs first instruction in the container
- Takes the image of the container and removes the container.
- Create another intermediate container and runs second instruction.
- That way it generated one layer and one temp container for each instrucation.
- If there is no change in layers, it will reuse it and wont rebuild.
- Best practise is to keep the instruction that change at the end.
