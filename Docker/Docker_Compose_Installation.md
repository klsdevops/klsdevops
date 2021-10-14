# docker-compose install:

## Copy the appropriate docker-compose binary from GitHub:

```
sudo curl -L https://github.com/docker/compose/releases/download/1.22.0/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
```

![image](https://user-images.githubusercontent.com/90503660/137363492-8f96ddff-d4a9-4457-af42-432aad49cd0f.png)

**NOTE:** to get the latest version 

```
sudo curl -L https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
```

## Set permissions after download:

```
sudo chmod +x /usr/local/bin/docker-compose
```

![image](https://user-images.githubusercontent.com/90503660/137363839-9fdc222a-9a74-458a-a4c3-9fa6b0ba2246.png)

## Verify the installation status

```
docker-compose version
```

![image](https://user-images.githubusercontent.com/90503660/137363954-389b05d3-5061-450b-9580-42d72d14b12b.png)
