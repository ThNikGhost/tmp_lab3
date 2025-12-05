# Demo — Python CI/DevSecOps

Минимальный проект для проверки пайплайнов Практики 3.

## Локальный запуск

```bash
# Сборка образа
docker build -t app:ci .

# Тесты в контейнере
docker run --rm -e PYTHONUNBUFFERED=1 app:ci pytest -q

# Pre-commit локально
python -m pip install --upgrade pip pre-commit
pre-commit run -a --show-diff-on-failure
```

## GitHub Actions
- Конфиг: `.github/workflows/ci.yml`
- Включает: pre-commit, Build/Test, Gitleaks, Semgrep, Trivy FS/Image, загрузку SARIF в Code Scanning.

## GitLab CI
- Конфиг: `.gitlab-ci.yml`
- Включает: pre-commit, Build/Test, Gitleaks, Semgrep, Trivy FS/Image, артефакты SARIF.

## Сценарии демонстрации
1. Добавьте заведомо уязвимую зависимость в requirements.txt → ожидается провал Trivy FS.
2. Добавьте хардкод секрета в код → ожидается провал Gitleaks/Semgrep.
3. Исправьте и добейтесь «зелёного» статуса CI.
