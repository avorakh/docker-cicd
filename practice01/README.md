#Commands

1. Build the first container
```bash
docker build -t practice01 .
```
2. Run the first container
```bash
# ${PWD} - current directory
# ${PWD}/ro:/root/ro:ro - the 'ro' folder will be mount to the '/root/ro' path with read-only acccess
docker run -it -v ${PWD}/dir:/dir -v ${PWD}/ro:/root/ro:ro practice01 
```
3. Copy file to container
```bash
mkdir tmp_dir
echo "File to copy from local to container" >> tmp_dir/copy_file.txt
# docker cp PATH/TO/file CONTAINER_ID:PATH/TO/file
docker cp tmp_dir/copy_file.txt 700c9224f706:/dir/moved_file.txt
```
4. Execute command in container
```bash
# docker exec CONTAINER_ID /bin/ls  -lah /root/
docker exec 700c9224f706 /bin/ls  -lah /root/
# to move in container
docker exec -it 700c9224f706 /bin/bash 
```
5. Inspect
```bash
docker inspect practice01 
```
6. Find unused images
```bash
docker images -f "dangling=true"
# only image IDs 
docker images -f "dangling=true" -q
# remove all unused images
docker rmi -f $(docker images -f "dangling=true" -q)
```
7. Remove unused resources 
```bash 
docker system prune
```
8. Run the last container
```bash 
docker run -it -v ${PWD}/dir:/dir -v ${PWD}/ro:/root/ro:ro -p 10000:10000 practice01_v7
```
 