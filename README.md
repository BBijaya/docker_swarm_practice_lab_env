# Docker Swarm Practice Lab Environment
Docker swarm practice lab environment setup using vagrant file

<hr ./>
<br>

## How to setup the local lab ?
### Pull the repo 
```sh
git clone [https://github.com/BBijaya/docker_swarm_practice_lab_env.git](https://github.com/BBijaya/docker_swarm_setup.git)
```
<br>

### Install vagrant and virtualbox
```sh
sudo apt install virtualbox vagrant -y
```
<br>

### Bring the vm's up

```sh
cd docker_swarm_practice_lab_env
```

```sh
vagrant up
```
<br>

### There  are 3 vm's setup by the default. **docker-master**,  **docker-worker1** and **docker-worker2**
<table>
    <thead>
        <tr>
            <th> Machine </th>
            <th> IP</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>docker-master</td>
            <td>172.16.0.5</td>
        </tr>
    </tbody>
    <tbody>
        <tr>
            <td>docker-worker1</td>
            <td>172.16.0.6</td>
        </tr>
    </tbody>
    <tbody>
        <tr>
            <td>docker-worker2</td>
            <td>172.16.0.7</td>
        </tr>
    </tbody>
</table>
<br>

### You can ssh into the vm using
**vagrant ssh \<machine-name>**
```sh
vagrant ssh docker-master
vagrant ssh docker-worker1
vagrant ssh docker-worker2
```
<br>

### Initialize docker swarm
```sh
vagrant ssh docker-master
docker swarm init --advertise-addr 172.16.0.5
```
<br>

### Join the swarm
<p> copy the command to join from the output of previous command and run in the each of worker node.
</p>

```sh
docker swarm join --token <token> 172.16.0.5:2377
```

<br>

### List the nodes from master

```sh
docker node ls 
```
<p> If it list all three nodes, the setup is ready!</p>
<p> Once you are done with the practice exit from the vm's and run, below comman to stop the vm's <p>

```sh
vagrant halt
```
<br>

### Get rid of the VM's
When you are done wit the lab you can delete the vm's using **vagrant destroy**. Also if you need it again you can alaway bring up the vm's using **vagrant up**.

```sh
vagrant destroy
```

