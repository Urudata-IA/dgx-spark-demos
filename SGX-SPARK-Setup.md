# Antes de comenzar 

Antes de comenzar a trabajar con la DGX Spark es importante ordenar los cachés de modelos, estos se manejan de diferente forma en los playbooks de la plataforma 
y eso hace que un mismo modelo sea bajado en diferentes directorios para las demos, algunas veces dentro de un container, otras en el file system, otras en el 
repositorio propio que maneja una herramienta.

Algunas de estas descargas duplicadas no las podemos evitar, ya que hay modelos preparados por los proveedores de los runtimes y difieren del modelo original
aunque sean de la misma versión, tamaño y cuantización, igual es una versión diferente del modelo, preparada, por ejemplo, por Ollama

Además de ajustar los lugares donde van estos modelos, tendremos también que ajustar las demos, para que respeten estos cachés, los dos que vamos a manejar con
especial cuidado son el de Huggingface y el de Nvidia. Para eso, tendermos que ajustar en general las creaciones de containers y configuraciones de las demos.

El primer paso, es definir en /etc/environment la configuración de las variables de entorno más relevantes
```bash
export HF_HOME=/cache/huggingface
export LOCAL_NIM_CACHE=/cache/nim
export NGC_API_KEY=nvapi-..... Key de NVIDIA de la DGX

#algunos demos y containers de NIM refieren a esta misma clave con otro nombre, así que hay que definirla dos veces, es el camino más corto
export NGC_CLI_API_KEY=nvapi-..... Key de NVIDIA de la DGX
```

Recomendado, cargar ya un token de HF por defecto para simplificar las demos, aunque algunos modelos necesitan de aceptar la licencia y en ese caso es 
mejor cargarlo en la sesión de cada usuario

```bash
export HF_TOKEN="SU TOken de HF"
export WANDB_API_KEY="Su Token de w&B"
```
