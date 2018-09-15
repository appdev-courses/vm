# vm
Docker setup to simulate a virtual machine for development purposes.

## Running the dev VM

First, set up [Docker](https://www.docker.com/get-started).

On a Unix system, simply execute `./vm_run` to initialize and run the development virtual machine.

`vm_run rebuild` rebuilds the VM from the Dockerfile, leaving data intact.
`vm_run reset` will rebuild the VM and recreate the data volume. VM data will be lost!

### Manual setup

To recreate the data volume (VM data will be lost!):
    
    docker rm vm-data # skip for initial setup
    docker create -v /home/vm-user --name vm-data busybox /bin/true

To rebuild the VM container:

    docker rm vm-container # skip for initial setup
    docker rmi vm-image    # skip for initial setup
    docker build . -t vm-image
    docker run -it --volumes-from vm-data --name vm-container vm-image /tmp/vm_init 

To rerun the VM after exiting (data will be preserved):

    docker attach vm-container

