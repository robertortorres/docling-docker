# Docling Serve com Docker Compose

Este projeto utiliza o Docker Compose para rodar o [Docling Serve](https://github.com/docling-project/docling-serve), uma interface para exploração de dados linguísticos, com suporte a GPU.

## Pré-requisitos

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)
- Driver da NVIDIA e [NVIDIA Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html) (para uso com GPU)

## Estrutura

Este `docker-compose.yaml` define um serviço:

### Serviço: `docling`

- **Imagem:** `ghcr.io/docling-project/docling-serve-cu124`
- **Porta exposta:** `5001:5001`
- **Interface web:** [http://localhost:5001](http://localhost:5001)
- **Volume montado:** `/storage/docling` no host montado em `/app/data` no container
- **Variáveis de ambiente:**
  - `DOCLING_SERVE_ENABLE_UI=true` — habilita a UI
- **Uso de GPU:** configurado para usar todas as GPUs disponíveis no host

## Como usar

1. Crie o diretório de dados no host (se ainda não existir):

   ```bash
   mkdir -p /storage/docling
   ```

2. Suba o container:

   ```bash
   docker compose up -d
   ```

3. Acesse a interface em: [http://localhost:5001](http://localhost:5001)

## Notas

- Se estiver usando GPU, certifique-se de que o driver NVIDIA e o container toolkit estão corretamente instalados.
- A linha `runtime: nvidia` está comentada. Você pode descomentar caso necessário para sua configuração específica.

## Parar o serviço

```bash
docker compose down
```
