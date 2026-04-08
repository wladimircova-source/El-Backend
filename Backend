from flask import Flask, request, jsonify
from datetime import datetime

app = Flask(__name__)

# Simulación de base de datos en memoria para los vagones detectados
registros_vagones = []

@app.route('/rfid/recepcion', methods=['POST'])
def recibir_dato():
    data = request.json
    # Estructura típica que envía una lectora industrial (EPC, Antena, Timestamp)
    nuevo_registro = {
        "tag_id": data.get("epc"),
        "antena": data.get("antenna"),
        "hora": datetime.now().strftime("%H:%M:%S"),
        "fecha": datetime.now().strftime("%d-%m-%Y"),
        # Aquí podrías cruzar con una DB para obtener el ID real del vagón
        "vagon_nro": f"VAG-{data.get('epc')[-4:]}" 
    }
    
    registros_vagones.insert(0, nuevo_registro) # Agregar al inicio
    return jsonify({"status": "success", "message": "Registro recibido"}), 200

@app.route('/api/vagones', methods=['GET'])
def obtener_vagones():
    return jsonify(registros_vagones[:10]) # Retorna los últimos 10

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
