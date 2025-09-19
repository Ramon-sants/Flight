# Flight
PIBICWORK
# ROS2 ↔ FlightGear Bridge

Este projeto faz a ponte entre ROS2 (Jazzy, Python) e o simulador FlightGear via UDP.

## Estrutura

- `ros2_control_node.py`: Nó ROS2 que escuta comandos no tópico `flightgear_command` e envia ao FlightGear por UDP.
- `flightgear_udp_sender.py`: Função para envio de comandos UDP ao FlightGear, utilizando configuração de IP/porta.
- `config/flightgear_udp.yaml`: Arquivo de configuração para IP/porta do FlightGear.

## Instalação e Uso

1. **Instale dependências:**
   - ROS2 Jazzy
   - Python 3.8+
   - Instale dependências Python:
     ```bash
     pip install rclpy std_msgs pyyaml
     ```

2. **Inicie o FlightGear recebendo UDP:**
   ```bash
   fgfs --generic=socket,in,10,localhost,5500,udp
   ```

3. **Configure IP/porta em `config/flightgear_udp.yaml` se necessário.**

4. **Execute o nó ROS2:**
   ```bash
   ros2 run ros2_flightgear_bridge ros2_control_node.py
   ```
   Ou, se estiver fora de um pacote ROS2, apenas:
   ```bash
   python ros2_control_node.py
   ```

5. **Publique comandos no tópico ROS2:**
   ```bash
   ros2 topic pub /flightgear_command std_msgs/String "data: '0.1 0.0 0.0 0.8'"
   ```

## Referências

- [FlightGear Generic protocol](https://wiki.flightgear.org/Generic_protocol)
- [ROS2 Python Tutorials](https://docs.ros.org/en/ros2_tutorials/)
