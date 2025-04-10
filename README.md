import requests
import json
import time

def send_credentials(target_ip: str, target_port: int, username: str, password: str):
    url = f"http://{target_ip}:{target_port}/login"
    headers = {"Content-Type": "application/json"}
    data = {
        "username": username,
        "password": password,
        "timestamp": time.strftime("%Y-%m-%d %H:%M:%S")
    }
    try:
        response = requests.post(url, headers=headers, data=json.dumps(data), timeout=5)
        print(f"Respuesta del servidor: {response.status_code} - {response.text}")
    except requests.exceptions.RequestException as e:
        print(f"Error al enviar las credenciales: {str(e)}")

def main():
    target_ip = "127.0.0.1"  # Reemplaza con la IP de tu teléfono
    target_port = 80
    username = "usuario1"
    password = "contraseña123"
    print(f"Enviando credenciales a {target_ip}:{target_port}...")
    send_credentials(target_ip, target_port, username, password)

if __name__ == "__main__":
    main()
