namespace Custommvc.Controllers
{
    public class HomeController : Controller
    {
        Uri apiUrl = new Uri("http://localhost:5126/WeatherForecast/");
        HttpClient Client;
        public HomeController()
        {

            Client = new HttpClient();
            Client.BaseAddress = apiUrl;
        }
        public IActionResult Index()
        {
            Client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", "eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJJZCI6IjBmOTQ2NDNmLWU0NjItNGE0Ny04ZGVhLTQzYzdiMGYyOTA2NiIsInN1YiI6ImthcmFuIiwiZW1haWwiOiJrYXJhbiIsImp0aSI6ImYwNGU3MDA1LWZmZWQtNDk5MS1hMzk5LWE3NzE0NDg1N2YwZCIsIm5iZiI6MTY4ODAxOTk1OSwiZXhwIjoxNjg4MDIwMjU5LCJpYXQiOjE2ODgwMTk5NTksImlzcyI6Imh0dHBzOi8vam95ZGlwa2FuamlsYWwuY29tLyIsImF1ZCI6Imh0dHBzOi8vam95ZGlwa2FuamlsYWwuY29tLyJ9.fGdJrcjRZPqlzyStbc1SJJ3q_6ZajSq3xYcLuZiYhTOz0lxDOl5zL7OkFin2jrL5YT-Ms7ssRPdIbH96yyR6jQ");
            HttpResponseMessage lis = Client.GetAsync(Client.BaseAddress + "GetData").Result;

       

            if (lis.IsSuccessStatusCode)
            {
                string data = lis.Content.ReadAsStringAsync().Result;
                 var result = JsonConvert.DeserializeObject<List<string>>(data);
            }
            return View();
        }
    }
}
