# Ansible Role: vector

Роль для автоматической установки и настройки [Vector](https://vector.dev/) — высокопроизводительного сборщика и маршрутизатора логов и метрик.

## Описание

Роль выполняет полную установку Vector из официальных RPM-пакетов и настраивает его для сбора логов с последующей отправкой в ClickHouse. Роль автоматизирует процесс скачивания пакета, установки, создания конфигурации и запуска сервиса.

## Требования

* **Ansible >= 2.9**
* **Python >= 3.6** на управляющем хосте
* **DNF** пакетный менеджер на целевых хостах (CentOS 8+, RHEL 8+, Fedora)

## Переменные роли

Все переменные для настройки роли хранятся в файле `defaults/main.yml`. Ниже приведена таблица с описанием каждой переменной.

| Имя | Значение по умолчанию | Описание |
|-----|----------------------|----------|
| `vector_version` | `"0.38.0"` | Версия Vector для установки |
| `vector_package` | `"vector-{{ vector_version }}-1.x86_64.rpm"` | Имя RPM-пакета |
| `vector_download_url` | `"https://packages.timber.io/vector/{{ vector_version }}/vector-{{ vector_version }}-1.x86_64.rpm"` | URL для скачивания пакета |
| `vector_config_dir` | `"/etc/vector"` | Директория с конфигурацией Vector |
| `vector_config_file` | `"{{ vector_config_dir }}/vector.yaml"` | Путь к файлу конфигурации |
| `vector_clickhouse_host` | `"localhost"` | Хост ClickHouse для отправки логов |
| `vector_clickhouse_database` | `"logs"` | Имя базы данных ClickHouse |
| `vector_clickhouse_table` | `"vector_messages"` | Имя таблицы ClickHouse |

## Пример плейбука

```yaml
- hosts: vector
  become: true
  roles:
    - vector-role