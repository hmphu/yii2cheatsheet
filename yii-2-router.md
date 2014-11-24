# Yii Framework 2 Router #
Routing involves two steps. In the first step, the incoming request is parsed into a route and the associated query parameters. In the second step, a controller action corresponding to the parsed route is created to handle the request.
## Default Route ##
    [
	    // Your configuration file
	    'defaultRoute' => 'main/index',
    ];
## catchAll Route ##
    [
	    // Your configuration file
	    'catchAll' => ['site/offline'],
    ];
## Request Parameters ##
	use Yii;
    $request = Yii::$app->request;
    $get = $request->get(); 
    // equivalent to: $get = $_GET;
    
    $id = $request->get('id');   
    // equivalent to: $id = isset($_GET['id']) ? $_GET['id'] : null;
    
    $id = $request->get('id', 1);   
    // equivalent to: $id = isset($_GET['id']) ? $_GET['id'] : 1;
    
    $post = $request->post(); 
    // equivalent to: $post = $_POST;
    
    $name = $request->post('name');   
    // equivalent to: $name = isset($_POST['name']) ? $_POST['name'] : null;
    
    $name = $request->post('name', '');   
    // equivalent to: $name = isset($_POST['name']) ? $_POST['name'] : '';
When implementing RESTful APIs, you often need to retrieve parameters that are submitted via PUT, PATCH or other request methods. You can get these parameters by calling the yii\web\Request::getBodyParam() methods. For example,
	use Yii;
    $request = Yii::$app->request;
    // returns all parameters
    $params = $request->bodyParams;
    
    // returns the parameter "id"
    $param = $request->getBodyParam('id');
## Request Methods ##
	use Yii;
    $request = Yii::$app->request;    
    if ($request->isAjax) { // the request is an AJAX request }
    if ($request->isGet)  { // the request method is GET }
    if ($request->isPost) { // the request method is POST }
    if ($request->isPut)  { // the request method is PUT }
## HTTP Headers ##
    // $headers is an object of yii\web\HeaderCollection 
    $headers = Yii::$app->request->headers;
    
    // returns the Accept header value
    $accept = $headers->get('Accept');
    
    if ($headers->has('User-Agent')) { // there is User-Agent header }
## Client Information ##
    $userHost = Yii::$app->request->userHost;
    $userIP = Yii::$app->request->userIP;