# System requirements

{% include [system-requirements](../_includes/speechkit/system-requirements.md) %}

{% include [system-requirements](../_includes/speechkit/system-requirements-gpu.md) %}

## Software requirements {#software}

A server dedicated for {{ sk-hybrid-name }} should enable running containers based on CUDA® 11.4 and higher and have the appropriate NVIDIA drivers. For more information about the CUDA Toolkit requirements, see the [official NVIDIA documentation](https://docs.nvidia.com/cuda/cuda-toolkit-release-notes/index.html).

To install and configure {{ sk-hybrid-name }} services, you need the {{ yandex-cloud }} CLI and a registry in {{ container-registry-full-name }}.

1. {% include [cli-install](../_includes/cli-install.md) %}

1. [Create a registry](../iot-core/operations/registry/registry-create.md) in {{ container-registry-full-name }}.

   {% include [default-catalogue](../_includes/default-catalogue.md) %}

   ```bash
   yc container registry create --name speechkit-hybrid
   ```

   Result:
   ```text
   id: crpc9qeoft236r8tfalm
   folder_id: b1g0itj57rbjk9thrinv
   name: speechkit-hybrid
   status: ACTIVE
   created_at: "2021-08-25T12:24:56.286Z"
   ```

1. Notify the {{ speechkit-name }} team of the created registry's `id`. All the required containers will appear in your registry, and you'll be provided `docker-compose.yaml`.
