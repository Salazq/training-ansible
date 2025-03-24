# training-ansible

### Archivos modificados:

- "hosts.ini": se puso la dirección IP de la VM que estaba corriendo y las credenciales para acceder a esta.
- "run_container.yml": se definió una tarea para levantar el contenedor junto con la imágen correspondiente y los puertos asignados.

## Actualizacion de permisos de puertos de la VM:
```
az network nsg rule create \
  --resource-group win-vm-iis-goldfish-rg \
  --nsg-name win-vm-iis-goldfish-nsg \
  --name AllowSSH \
  --priority 1100 \
  --direction Inbound \
  --access Allow \
  --protocol Tcp \
  --source-port-range '*' \
  --destination-port-range 22 \
  --source-address-prefix '*' \
  --destination-address-prefix '*'
```

```
az network nsg rule create \
  --resource-group win-vm-iis-goldfish-rg \
  --nsg-name win-vm-iis-goldfish-nsg \
  --name Allow-Mario \
  --protocol Tcp \
  --priority 1002 \
  --destination-port-range 8787 \
  --access Allow \
  --direction Inbound
```

## Instalar docker:

`ANSIBLE_HOST_KEY_CHECKING=False ANSIBLE_ROLES_PATH=./roles ansible-playbook -i inventory/hosts.ini playbooks/install_docker.yml`

## Correr contenedor:
`ANSIBLE_HOST_KEY_CHECKING=False ANSIBLE_ROLES_PATH=./roles ansible-playbook -i inventory/hosts.ini playbooks/run_container.yml`




## Consola de la VM:

![image](https://github.com/user-attachments/assets/ada000f3-b143-4118-9366-9116f08d82a3)


## Web:

![image](https://github.com/user-attachments/assets/641854ea-58c5-4ab1-a54e-5ac06471a8a0)
