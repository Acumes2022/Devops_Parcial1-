


ejercicio 1

se debe tener descargado el repositorio y tambien instalado visual studio, ansible, doctl, terraform y tener una cuenta activa en digital ocean

desde el host es necesario crear una llave publica para pegarla en digital ocean. 
se debe generar un tocken en digital ocean para pegarlo en el archivo tfvars
tambien es necesario generar el id key, esto se genera con el comando doctl  -t [TOKEN] compute ssh-key list. el id tambine se se pega en el archivo  .tfvars en droplet_ssh_key_id

- se utiliza terraform init para iniciar terraform.
- ahora se puede verificar el plan que se ejecuta, con terraform plan
- para aplicar el codigo  y que los servicios se creen en digital ocean es necesario utilizar el comando terraform apply
- para confirmar que ya todo esta configurado correctamente, se puede consultar la ip publica que nos devuelve el codigo, desde un navegador web.
- Cuando ya se tiene todo funcionando, se utiliza terraform destroy para eliminar todo de digital ocean.


ejercico 2
se debe tener descargado el repositorio y tambien instalado vmware, visual studio y vagrant.

- correr vagrant up para levantar las vm
- con el comando vagrant status se puede ver las maquinas virtuales creadas. en mi caso las maquinas virtuales creadas son:

hostname1 - running (virtualbox)
hostname2 - running (virtualbox)

- cuando ya se tienne las maquinas virtuales instaladas, se ingresa a la primer maquina por el comando vagrant ssh hostname1
- revisar que docker se encuentre instalado con el comando docker version
- ahora se inicia docker con el comando docker swarm init --advertise-addr 10.10.10.1:2377
- en este momento, se recibe el tocken que se utilzara en el servidor hostname2 
- se ingresa a la segunda maquina por el comando vagrant ssh hostname2
- se ejecuta el comando docker swarm agreganndo el token obtenido anteriormente
 docker swarm join \
    --token SWMTKN-1-2ynpq8ah9m5vkzfmg051gc4bsbf530r3wkt2k9b59gj4p4jepi-etj3dlx2h8ab14kexwmjn0p6d \
    10.10.10.1:2377
- con esto se une el nodo a swarm como un worker.
- ahora nuevamente conectar via ssh a la vm hostname1 y ejecutar docker node ls, esto mostrara los dos nodos creados.
 