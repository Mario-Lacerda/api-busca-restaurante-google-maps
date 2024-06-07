# Desafio Dio - Criando um Site para Encontrar Restaurantes Usando Google Maps que Consulta API do Google



### **Criando um Site para Encontrar Restaurantes Usando Google Maps que Consulta API do Google**



Este tutorial irá guiá-lo pelo processo de criação de um site que permite aos usuários encontrar restaurantes usando a API do Google Maps. O site incluirá um formulário de pesquisa onde os usuários podem inserir um termo de pesquisa (por exemplo, nome do restaurante, tipo de comida) e receberão uma lista de restaurantes correspondentes com informações como nome, endereço, classificação e horário de funcionamento.



#### **Pré-requisitos**

- Conhecimento básico de HTML, CSS e JavaScript
- Conta do Google Cloud Platform
- Chave de API do Google Maps



#### **Passo 1: Criar um Site HTML**

Crie um novo arquivo HTML e inclua o seguinte código básico:

plaintext

```plaintext
<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Busca de Restaurantes</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>Busca de Restaurantes</h1>
  <form id="search-form">
    <input type="text" id="search-input" placeholder="Nome do restaurante ou tipo de comida">
    <input type="submit" value="Buscar">
  </form>
  <div id="results"></div>
  <script src="script.js"></script>
</body>
</html>
```



#### **Passo 2: Conectar à API do Google Maps**

Para conectar seu site à API do Google Maps, você precisará obter uma chave de API. Siga estas etapas:

1. Acesse o site da API do Google Maps.
2. Clique em "Obter uma chave de API".
3. Crie ou selecione um projeto existente.
4. Clique em "Criar".



Copie a chave de API gerada e adicione-a ao seu arquivo HTML, substituindo `YOUR_API_KEY`:

plaintext

```plaintext
<script src="https://maps.googleapis.com/maps/api/js?key=YOUR_API_KEY"></script>
```



#### **Passo 3: Criar a Função de Pesquisa**

Crie um arquivo JavaScript (`script.js`) e adicione a seguinte função:

javascript

```javascript
function searchRestaurants(query) {
  // Crie uma consulta do Google Maps.
  const request = {
    query: query,
    location: 'current_location', // Use a localização atual do usuário ou especifique uma localização manualmente
    radius: '500', // Raio da pesquisa em metros (opcional)
    type: 'restaurant', // Tipo de local a ser pesquisado (opcional)
  };

  // Crie um serviço de lugares do Google Maps.
  const service = new google.maps.places.PlacesService(document.createElement('div'));

  // Execute a consulta.
  service.textSearch(request, (results, status) => {
    if (status === google.maps.places.PlacesServiceStatus.OK) {
      displayResults(results);
    } else {
      alert('Erro na pesquisa: ' + status);
    }
  });
}
```



#### **Passo 4: Exibir os Resultados**

Modifique o arquivo `index.html` para exibir os resultados da pesquisa:

plaintext

```plaintext
<div id="results">
  <ul>
  </ul>
</div>
```



Adicione o seguinte código ao arquivo JavaScript para exibir os resultados na lista:

javascript

```javascript
function displayResults(results) {
  const resultList = document.querySelector('#results ul');

  results.forEach((result) => {
    const formattedAddress = result.formatted_address;
    const name = result.name;
    const rating = result.rating;
    const openingHours = result.opening_hours ? result.opening_hours.weekday_text : 'Horário de funcionamento não disponível';

    const listItem = document.createElement('li');
    const listItemHeading = document.createElement('h3');
    const listItemAddress = document.createElement('p');
    const listItemRating = document.createElement('p');
    const listItemHours = document.createElement('p');

    listItemHeading.textContent = name;
    listItemAddress.textContent = formattedAddress;
    listItemRating.textContent = `Classificação: ${rating}`;
    listItemHours.textContent = `Horário de funcionamento: ${openingHours}`;

    listItem.appendChild(listItemHeading);
    listItem.appendChild(listItemAddress);
    listItem.appendChild(listItemRating);
    listItem.appendChild(listItemHours);

    resultList.appendChild(listItem);
  });
}
```



#### **Passo 5: Adicionar Manipulador de Eventos de Pesquisa**

Adicione um manipulador de eventos de envio ao formulário de pesquisa:

javascript

```javascript
const form = document.getElementById('search-form');

form.addEventListener('submit', (e) => {
  e.preventDefault();

  const query = document.getElementById('search-input').value;

  searchRestaurants(query);
});
```



#### **Passo 6: Testar o Site**

Salve todos os arquivos e abra o arquivo HTML em um navegador. Digite um termo de pesquisa e clique em "Buscar". Os resultados da pesquisa devem ser exibidos na lista.



### **Observações:**

- Você pode personalizar a aparência e o comportamento do site editando os arquivos HTML e CSS.
- A chave de API do Google Maps tem um limite de uso diário. Monitore seu uso e atualize a chave se necessário.
- Para obter recursos adicionais, consulte a documentação da API do Google Maps





<h3>Tecnologias utilizadas</h3>

- [HTML](https://www.w3schools.com/html/)
- [CSS](https://developer.mozilla.org/pt-BR/docs/Web/CSS)
- [JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript)<br>

<!--License session-->
<h3>Licença</h3>

- Este projeto está sob a licença [MIT](./LICENSE).<br>

<!--Bottom session-->
<br><h4 align=center>Made with by <a target="_blank" href="https://pleiterson.vercel.app" >Pleiterson Amorim</a></h4>