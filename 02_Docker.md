# Docker
## Dockerfile
Commands to build an image.

Stappen
- Specify base image ```FROM ...```
- Copy some files ```COPY . .```
- Install programs ```RUN dotnet build```
- Specify startup command ```ENTRYPOINT ["dotnet", "mydotnetapp.dll"]```

### Layers
Bij elke RUN, COPY, ADD wordt er een nieuwe laag toegevoegd aan de image.

Wanneer we images gaan builden, wordt de laag gecached.

- We passen enkel de source code aan.
- Dependencies laten we onveranderd.
- **Dependencies worden toch geïnstalleerd!**

+ **Waarom?** Omdat we maar 1 keer copy gebruiken, is de laag veranderd en kan er geen cache gebruikt worden.

+ **Betere manier:** 
```Dockerfile
 # Laag 1 = onveranderd = cache gebruiken
COPY *.csproj .
RUN dotnet restore

# Laag 2 = veranderd = geen cache
COPY . .
RUN dotnet publish -c release -o /app
```

## Building containers
```docker build . [-t repository/image:tag]```

Build process:
- Gebruikt cache waar mogelijk (sneller) 
- Using intermediate containers
- Volgorde doet ertoe!

```docker commit . -c <startup command>```

Image maken van een bestaande container

## Docker images
- ```docker pull <image name>``` downloading image (layers)
- ```docker pull mariadb``` officiële image
- ```docker pull boussonkarel/custom-img``` boussonkarel = repository, custom-img = image
- ```docker pull python:3.10-alpine``` image tagging = specifieke versie

*Extra: alpine Linux vaak kleiner dan andere.*

## Docker registes
- Docker registry server
  - Docker Hub server
  - AWS, Azure...
  - Github Container Registry (GHCR)
  - Bring Your Own Registry
- Private registries need login credentials
- Default = Docker hub

## Running containers
```docker run <image name> <alternative command>```
- Wraps two commands in one
  - Docker create <image name>
  - Docker start <container id>

```docker stop (graceful) / docker kill (immediate)```

```docker ps ()-all)```

## Interacting & logs
- No GUI!
- ```docker exec -it <container id> <command>```
- ```docker logs <container id>```

## Docker-compose
Easier to run (multiple) containers

No huge list of parameters > Declarative yaml file.

```docker-compose up --build```

Meerdere containers met één command opstarten.

Relaties configureren: ```depends_on```
(Wachten met opstarten tot ander is opgestart)

### Image
```yaml
api: # Service name = naam voor container
  image: nathansegers/custom-api:latest # Image naam (om te pullen, of builden)
```

### Build
```yaml
  build: ./web/api # build ./web/api/Dockerfile
```

### Ports - Expose
```yaml
  # Externe port (laptop)
  # :
  # Interne port (container)
  ports:
    - 5000:80
    - 5001:443
```
```yaml
   # Exposen naar andere services binnenin netwerk
  expose:
    - 3306 # Toegankelijk binnen container
    - 5000
  
```

### Network
Alle services in een docker-compose zitten standaard in een netwerk. De service name is hun hostname in het netwerk, bv. ```http://api:3001```

Expose kun je niet bereiken met localhost, zaken met 'ports' wel.
### Volumes
- Zorgen voor persistent storage.
- Private files
- Secrets

In plaats van COPY of ADD!
```yaml
  volumes:
    - ./shared_data/:/mnt/data/shared # Relative/absolute paths
    - named_volume:/mnt/persistent/volume # Named volumes

volumes:
  named_volume: # Kan gedeeld worden tussen services
```
Environments
```yaml
  volumes:
    - ./shared_data/:/mnt/data/shared # Beide op laptop & container beschikbaar
    - named_volume:/mnt/persistent/volume

volumes:
  named_volume: # Kan gedeeld worden tussen services
```

### Environments
Environment variabelen injecteren die gebruikt kunnen worden om andere settings te overscrijven.

Meer security, sharen van variabelen.

Typische taken:
- Connection Strings
- Port overrides
- Production or Development mode
```yaml
api:
  env_file:
    - .env
  environment:
    - API_PORT=8080
    - MODE=Production
    - MYSQL_XXX=YYYY
```

### Depends_on
Service A wacht tot de andere service B is opgestart.