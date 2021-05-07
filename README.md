# idkk
idk
use Tmont\Phroxy\Interceptor;
use Tmont\Phroxy\InterceptorCache;
use Tmont\Phroxy\InterceptionContext;
use ReflectionClass;

class ReturnBeforeCallInterceptor implements Interceptor {
	public function onBeforeMethodCall(InterceptionContext $context) {
		$context->setReturnValue('oh hai!');
	}

	public function onAfterMethodCall(InterceptionContext $context) {}
}

class MyClass {
	public function hello() {
		return 'hello';
	}
}

$interceptor = new ReturnBeforeCallInterceptor();
InterceptorCache::registerInterceptor($interceptor, function($x) { return true; });

$proxy = $this->builder->build(new ReflectionClass('MyClass'));
$proxy->hello(); // "oh hai!"
