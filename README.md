
## Entrar no node1


```
docker-compose exec node1 bash
>service ssh start
```

# Brincando Localmente

## Cria chave
```
ssh-keygen
cd /root/.ssh
```

# Vincula a chave para acessar
```
ssh-copy-id root@node1
ssh root@node1
cat /root/.ssh/authorized_keys  # São as chaves autorizadas a entar nessa máquina
```


### Ping todas as máquinas

```
ansible -i hosts all -m ping
```

### Ping em máquina específica
```
ansible -i hosts node1 -m ping
```

### Instalando Git em todas as máquinas
```
ansible -i hosts all -m apt -a "update_cache=yes name=git state=present"
ansible -i hosts -m git -a "repo=https://.com/codeeedu/fc2-terraform dest=/root/terraform-repo"
```

### Instalando nginx em todas as máquinas
```
ansible -i hosts all -m apt -a "update_cache=yes name=nginx state=present"
```

### Removendo nginx em todas as máquinas
```
ansible -i hosts all -m apt -a "update_cache=yes name=nginx state=absent"
```

# AWS

## Criar key Pair
```
aws ec2 create-key-pair --endpoint=http://localhost:4566 --key-name MyKeyPair --query 'KeyMaterial' --output text > MyKeyPair.pem
```

## Criar EC2 Instances
```
aws ec2 run-instances --endpoint=http://localhost:4566 --image-id ami-amazon-linux-latest --count 1 --instance-type t2.micro --key-name MyKeyPair --security-group-ids sg-903004f8 --subnet-id subnet-6e7f829e
```

### Listando EC2
```
aws ec2 describe-instances --endpoint=http://localhost:4566
```

### Rodando playbook

```
ansible-playbook -i hosts playbook.yaml
```

# Ansible Galaxy

```
ansible-galaxy init install-nginx
```

## Docker Swarm
É como se fosse um kubernetes, subir a mesma aplicações em múltiplos containers
