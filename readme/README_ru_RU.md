# знания

**Автор:** hjlarry  
**Версия:** 0.0.2  
**Тип:** инструмент  
**Репозиторий:** [https://github.com/hjlarry/dify-plugin-knowledge](https://github.com/hjlarry/dify-plugin-knowledge)  

## Начало работы

### 1. Авторизация

API_URL и API_KEY берутся отсюда:  
![1](./_assets/1.png)

### 2. Конфигурация

![2](./_assets/2.png)

ID набора данных берётся отсюда:  
![3](./_assets/3.png)

`PROCESS RULE` может быть по умолчанию `{"mode": "automatic"}`, но если вы хотите настроить правила обработки, конфигурируйте следующим образом:

Когда ваш `CHUNK METHOD` — `General` или `Q&A`, `PROCESS RULE` должен быть таким:  
```json
{
  "mode": "custom",
  "rules":{
    "pre_processing_rules": [{"id":"remove_extra_spaces", "enabled": true}, {"id":"remove_urls_emails", "enabled": true}],
    "segmentation": {
      "separator": "\n\n",
      "max_tokens": 1024,
      "chunk_overlap": 50
    }
  }
}
```

Когда ваш `CHUNK METHOD` — `Parent-child`, `PROCESS RULE` должен быть таким:  
```json
{
  "mode": "hierarchical",
  "rules": {
    "pre_processing_rules": [
      {
        "id": "remove_extra_spaces",
        "enabled": true
      },
      {
        "id": "remove_urls_emails",
        "enabled": true
      }
    ],
    "segmentation": {
      "separator": "\n\n",
      "max_tokens": 1024,
      "chunk_overlap": 50
    },
    "parent_mode": "full-doc",
    "subchunk_segmentation": {
      "separator": "\n\n",
      "max_tokens": 1024,
      "chunk_overlap": 50
    }
  }
}
```

### 3. Запуск

Вы можете запустить плагин следующим образом, следуя примеру плагина парсинга PDF, такого как `MinerU`:  
![4](./_assets/4.png)