# Web Scraper em PHP usando cURL

![PHP Scraper](https://img.shields.io/badge/PHP-Scraper-blue.svg)

Este repositório contém um tutorial sobre como criar um web scraper em PHP utilizando `cURL`, definindo payload, headers e usando o método `GET`.

## 🚀 Requisitos

- PHP 7+ instalado
- Extensão cURL ativada
- Editor de código

## 📜 Passo a Passo

### 1️⃣ Criando o Arquivo do Scraper

Crie um arquivo `scraper.php` e adicione o seguinte código:

```php
<?php

function scrapeWebsite($url, $headers = [], $payload = []) {
    $ch = curl_init();
    
    // Se houver payload, adicione como query string
    if (!empty($payload)) {
        $url .= '?' . http_build_query($payload);
    }
    
    curl_setopt($ch, CURLOPT_URL, $url);
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
    curl_setopt($ch, CURLOPT_FOLLOWLOCATION, true);
    
    // Definir Headers personalizados
    if (!empty($headers)) {
        curl_setopt($ch, CURLOPT_HTTPHEADER, $headers);
    }
    
    // Executar a requisição
    $response = curl_exec($ch);
    
    // Verificar erros
    if (curl_errno($ch)) {
        echo 'Erro no cURL: ' . curl_error($ch);
        return false;
    }
    
    curl_close($ch);
    
    return $response;
}

// Exemplo de uso
$url = "https://jsonplaceholder.typicode.com/posts";
$headers = [
    "User-Agent: Mozilla/5.0",
    "Accept: application/json"
];
$payload = [
    "userId" => 1
];

$result = scrapeWebsite($url, $headers, $payload);

if ($result) {
    echo "Resultado da Scraping: \n";
    echo $result;
}
?>
```

### 📌 Explicação do Código

- **`curl_init()`**: Inicializa a sessão cURL.
- **Query string**: Se existir um payload, ele é convertido para query string e anexado à URL.
- **`CURLOPT_RETURNTRANSFER`**: Faz com que a resposta seja retornada como string em vez de ser impressa diretamente.
- **`CURLOPT_FOLLOWLOCATION`**: Segue redirecionamentos automáticos.
- **Headers**: Podem ser personalizados, incluindo User-Agent.
- **`curl_exec()`**: Executa a requisição HTTP.
- **Erros**: Se ocorrerem, são exibidos.

### ▶️ Executando o Scraper

Salve o arquivo e execute no terminal:

```sh
php scraper.php
```

Isso deve retornar os dados extraídos da URL informada.

## 🤖 Contribuindo

Sinta-se à vontade para abrir issues e pull requests com sugestões e melhorias.

## ⚠️ Aviso

Use este scraper com responsabilidade e siga as políticas dos sites que você acessar!

---

Feito com ❤️ por [walker](https://github.com/walkerGold)

