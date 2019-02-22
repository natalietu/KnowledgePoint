##### 一、 解决 Target [Illuminate\Contracts\Routing\ResponseFactory] is not instantiable

- [参考文档](https://stackoverflow.com/questions/41266764/target-illuminate-contracts-routing-responsefactory-is-not-instantiable)
- I am trying to return a response like this:

		return response()->json(['name' => 'Abigail', 'state' => 'CA']);
- however, I got error:

	`Target [Illuminate\Contracts\Routing\ResponseFactory] is not instantiable.`
	
- In bootstrap/app.php, uncomment the following line

		$app->register(App\Providers\AppServiceProvider::class);

- Then in app\Providers\AppServiceProvider.php, update register method to add:

		public function register()
		{
		    $this->app->singleton('Illuminate\Contracts\Routing\ResponseFactory', function ($app) {
		        return new \Illuminate\Routing\ResponseFactory(
		            $app['Illuminate\Contracts\View\Factory'],
		            $app['Illuminate\Routing\Redirector']
		        );
		    });
		}
