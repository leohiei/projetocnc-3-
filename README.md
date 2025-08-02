Aqui está um modelo de **README.md** para você colocar no GitHub, documentando o projeto com base no **código CNC**, **desenho** e **trajetória**:

---

# 🛠️ Projeto CNC – Usinagem de Peça com Dois Lados

Este projeto demonstra a usinagem completa de uma peça simétrica em torno CNC, utilizando **ciclos de desbaste (G71)** e **acabamento (G70)**, incluindo raios, chanfros e operações internas e externas.

---

## 📐 **Desenho da Peça**

A peça possui geometrias externas e internas, com raios de concordância e rebaixos.
**Dimensões principais:**

* Diâmetro externo: **Ø100 mm**
* Rebaixo: **Ø68 mm**
* Furos internos escalonados: Ø60 mm, Ø30 mm e Ø20 mm
* Raios: **R2** externos, **R3** internos
* Chanfros: **3 × 45°**
* Comprimento total: **62 mm**

![Desenho da Peça](usinagem-dois-lados-desenho.png)

---

## 🧭 **Trajetória de Ferramenta**

O caminho da ferramenta inclui:

* **Desbaste externo** com G71
* **Acabamento** com G70
* **Rebaixo interno** com novo G71
* **Operação de canal (bedame)**
* **Rosqueamento ou acabamento interno com compensação G41**

![Traçado da Usinagem](usinagem-dois-lados-tracado.png)

---

## 🔍 **Estrutura do Programa CNC**

O programa está dividido em etapas:

### **1. Preparação**

* Posição segura e seleção de ferramenta (`G53`, `T0101`)
* Ativação de velocidade de corte constante (`G96`)
* Limite de rotação (`G92`)

### **2. Desbaste Externo (G71)**

Define o contorno da peça com ciclos:

```gcode
N110 G71 U2 R2
N120 G71 P130 Q210 U0.4 W0.2 F.3
```

### **3. Acabamento Externo (G70)**

Chamada para o bloco do perfil:

```gcode
N320 G70 P130 Q210 F.2
```

### **4. Canal com Bedame**

Inclui parada (`M00`) e uso de ferramenta `T0505`.

### **5. Operação Interna**

Novo desbaste e acabamento:

```gcode
N660 G71 U2 R2
N670 G71 P680 Q710 U0.4 W0.2 F.3
```

### **6. Finalização**

* Cancelamento de compensações (`G40`)
* Retorno seguro (`G53`)
* Fim de programa (`M30`)

---

## ✅ **Código Completo**

```gcode
N10 G53 G00 X100 Z100 T00
N20 T0101
N30 G96 S200 M4
N40 G92 S22000
...
N1210 M30
```

*(Veja o arquivo `usinagem-dois-lados.nc` para o código completo.)*

---

## 🛠️ **Principais Recursos Utilizados**

* **Ciclos fixos**: G71 (desbaste), G70 (acabamento)
* **Compensações**: G41/G42
* **Interpretação de raios**: R2, R3
* **Contornos complexos** com arcos (G02/G03)
* **Operação de canal (bedame)**

---

## 💻 **Simulação**

Este projeto foi validado no **SwanSoft CNC** com controle **FANUC 0i-T**, incluindo:

* Verificação de colisões
* Teste de compensação de raio
* Ajuste de perfil com base no desenho técnico

---

### 🔗 **Arquivos incluídos**

* `usinagem-dois-lados.nc` → Código CNC completo
* `usinagem-dois-lados-desenho.png` → Desenho técnico
* `usinagem-dois-lados-tracado.png` → Caminho da ferramenta

