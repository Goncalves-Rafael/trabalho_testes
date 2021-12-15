## Testes da Classe - ProfileApiTest
O arquivo original pode ser encontrado [aqui](https://github.com/gothinkster/spring-boot-realworld-example-app/blob/master/src/test/java/io/spring/api/ProfileApiTest.java#L75).

### Setup

> Antes dos testes serem executados, alguns passos são realizados. Primeiro o objeto do tipo MockMvc que foi injetado é passado para a classe RestAssuredMockMvc através do método mockMvc, assim toda requisição realizada utilizará o objeto injetado. Em seguido dois objetos são instanciados, um de nome anotherUser do tipo User e outro profileData do tipo ProfileData, ambos serão utilizados nos testes a seguir. Por fim, o método findByUsername do objeto userRepository é mockado, para quando receber o username do objeto anotherUser, retornar um Optional encapsulando o objeto anotherUser.

### Teste 1: should_get_user_profile_success

> Este teste é responsável por verificar que ao realizar uma chamada do tipo get no endpoint "/profiles/{username}" passando um username válido, ele irá retornar uma resposta com código de status 200 (OK), contendo no corpo da requisição um objetivo profile com um campo username igual ao nome de usuário esperado. Para isso, o método findByUserName do serviço  profileQueryService é mockado, retornando um Optional com um ProfileData de um usuário válido, caso seja passado o username correto.

### Teste 2: should_follow_user_success

> Este teste é responsável por verificar que um usuário válido é capaz de realizar a operação de "seguir" outro usuário no sistema. Para isso, o método findByUserName do serviço  profileQueryService é mockado, retornando um Optional com um ProfileData de um usuário válido, caso seja passado o username correto. Em seguida, é realizada uma requisição do tipo POST com um token de autorização no endpoint "/profiles/{username}/follow" com um nome de usuário válido, seguido de uma asserção no código de status da resposta, com valor esperado 200 (OK). Em seguida, é verificado se o objeto userRepository tentou salvar uma nova relação do tpo FollowRelation envolvendo o usuário, provalmente obtido através do token, e o usuário passado na requisição.

### Teste 3: should_unfollow_user_success

> Este teste é responsável por verificar que um usuário válido que já segue outro usuário válido, ao chamar o serviço "follow" com o método delete, a remoção da relação FollowRelation será disparada. Aqui o mesmo mock é realizado como nos dois primeiros testes, porém o método findRelation do objeto userRepository também é mockado, retornando uma relação válida ao receber dois id's válidos de usuários. Em seguida, uma requisição com  um token de autorização do tipo delete no endpoint "/profiles/{username}/follow" com um nome de usuário válido é realizada, seguido de uma asserção no código de status da resposta, com valor esperado 200 (OK).
