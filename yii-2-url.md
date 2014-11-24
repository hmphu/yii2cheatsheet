# Yii Framework 2 URLs #
## Request URLs ##
Assuming the URL being requested is http://example.com/admin/index.php/product?id=100, you can get various parts of this URL as summarized in the following:

	use Yii;
    $request = Yii::$app->request;    
	$request->url; // admin/index.php/product?id=100
	$request->absoluteUrl; // http://example.com/admin/index.php/product?id=100
	$request->hostInfo; // http://example.com
	$request->pathInfo; // /product
	$request->queryString; // id=100
	$request->baseUrl; // /admin
	$request->scriptUrl; // admin/index.php
	$request->serverName; // example.com
	$request->serverPort; // 80
## Creating URLs ##
	use yii\helpers\Url;
	
	// creates a URL to a route: /index.php?r=post/index
	echo Url::to(['post/index']);
	
	// creates a URL to a route with parameters: /index.php?r=post/view&id=100
	echo Url::to(['post/view', 'id' => 100]);
	
	// creates an anchored URL: /index.php?r=post/view&id=100#content
	echo Url::to(['post/view', 'id' => 100, '#' => 'content']);
	
	// creates an absolute URL: http://www.example.com/index.php?r=post/index
	echo Url::to(['post/index'], true);
	
	// creates an absolute URL using the https scheme: https://www.example.com/index.php?r=post/index
	echo Url::to(['post/index'], 'https');