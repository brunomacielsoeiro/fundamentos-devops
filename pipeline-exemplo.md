# Exemplo de Pipeline

Um pipeline simples pode conter:

1. Build
2. Testes
3. Deploy

## Exemplo (GitHub Actions)

```yaml
name: CI Pipeline

on:
  push:
    branches: [ "main" ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout do código
        uses: actions/checkout@v3

      - name: Simular build
        run: echo "Build executado com sucesso"

      - name: Simular testes
        run: echo "Testes executados com sucesso"

      - name: Simular deploy
        run: echo "Deploy realizado"