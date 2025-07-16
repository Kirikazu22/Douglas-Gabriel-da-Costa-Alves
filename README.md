func send_python_code(code: String, fase):
	if code.strip_edges().length() < 2:
		print("Erro: Código muito curto ou vazio.")
		return

	print("Código válido enviado:", code)

	var body = JSON.stringify({"code": code, "fase": fase})
	var headers = ["Content-Type: application/json"]
	var url = ""

	if OS.has_feature("HTML5"):
		url = "https://godot-python-game.onrender.com/execute_code"
	else:
		url = "http://127.0.0.1:10000/execute_code"

	print("URL usada na requisição:", url)

	if not http_request:
		print("Erro: HTTPRequest não inicializado.")
		return

	var error = http_request.request(url, headers, HTTPClient.METHOD_POST, body)

	if error != OK:
		print("Erro na requisição HTTP:", error)
