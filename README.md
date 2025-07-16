var url = ""

# Detecta se estamos rodando no navegador via JavaScript
if Engine.has_singleton("JavaScript"):
	var js = JavaScript.get_singleton()
	var current_host = js.eval("window.location.origin", true)
	url = current_host + "/execute_code"
else:
	# Ambiente local, com servidor Flask rodando na porta 10000
	url = "http://127.0.0.1:10000/execute_code"

print("URL usada na requisição:", url)

# Garante que http_request foi adicionado corretamente à cena
if not http_request:
	print("Erro: HTTPRequest não inicializado.")
	return

var error = http_request.request(url, headers, HTTPClient.METHOD_POST, body)

if error != OK:
	print("Erro na requisição HTTP:", error)


E no _ready(), garanta que o http_request está configurado:

func _ready():
	http_request = HTTPRequest.new()
	add_child(http_request)
	http_request.request_completed.connect(_http_request_completed)
