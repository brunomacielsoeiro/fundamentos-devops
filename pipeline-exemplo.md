# Exemplo de Pipeline

Um pipeline simples pode conter:

1. Build
2. Testes
3. Deploy

## Exemplo (GitHub Actions)

```yaml
name: CI Pipeline

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v2

      - name: Build
        run: echo "Build executado"

      - name: Test
        run: echo "Testes executados"