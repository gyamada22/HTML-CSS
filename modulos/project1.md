```
# 📊 Projeto — Dashboard de Hábitos Pessoais

## 🎯 Objetivo

Criar um banco de dados pessoal de hábitos que poderá ser usado futuramente
para construir um dashboard interativo com gráficos, correlações e insights
sobre sua rotina.

A ideia é registrar dados simples diariamente e depois usar tecnologias como:
  - Python        (análise de dados)
  - SQL           (armazenamento)
  - HTML+CSS      (visualização no site)

Com o tempo, você poderá descobrir padrões como:
  - relação entre sono e produtividade
  - impacto da academia no humor
  - quantas horas você realmente estuda por semana
  - equilíbrio entre estudo e lazer

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

# 🧠 Tipos de Dados a Registrar

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## 💤 Sono

O sono é um dos dados mais importantes porque afeta:
  energia / foco / produtividade / humor

  hora_dormir   →  ex: 00:30
  hora_acordar  →  ex: 08:00
  sono_horas    →  ex: 7.5

Análises futuras:
  - média de horas de sono
  - dias com menos de 7h
  - relação entre sono e horas de estudo

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## 📚 Estudo

Registrar estudo ajuda a visualizar sua evolução em programação.

  estudo_horas       →  ex: 4
  conteudo_estudo    →  ex: HTML + CSS
  dificuldade_estudo →  ex: 3  (escala 1–5)

Análises futuras:
  - horas estudadas por semana
  - tecnologias mais estudadas
  - evolução ao longo dos meses

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## 🏋️ Academia

A bike fornece métricas úteis para análise.

  academia     →  ex: sim
  tipo_treino  →  ex: bike
  tempo_treino →  ex: 20min
  calorias     →  ex: 140
  bike_km      →  ex: 6.2

Análises futuras:
  - km pedalados por semana
  - calorias queimadas
  - frequência de treino

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## 🍽️ Alimentação (horários)

Apenas os horários — sem registrar o que comeu.

  hora_cafe   →  ex: 09:00
  hora_almoco →  ex: 13:00
  hora_jantar →  ex: 20:00

Análises futuras:
  - intervalos entre refeições
  - relação entre jantar tarde e qualidade do sono

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## 🎮 Lazer

Equilíbrio entre produtividade e descanso.

  lazer_horas →  ex: 2
  tipo_lazer  →  ex: filme

Análises futuras:
  - proporção estudo vs lazer
  - tipos de lazer mais comuns

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## ⚡ Energia / Humor

Dado subjetivo, muito útil para correlações.

  1 = muito cansado
  2 = cansado
  3 = normal
  4 = bem
  5 = muito bem

  energia_dia →  ex: 4

Análises futuras:
  - relação entre sono e energia
  - impacto da academia no humor

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

# 🗂️ Estrutura do Banco de Dados (SQL)

  data               DATE
  hora_dormir        TIME
  hora_acordar       TIME
  sono_horas         FLOAT
  estudo_horas       FLOAT
  conteudo_estudo    TEXT
  dificuldade_estudo INT     -- 1 a 5
  academia           BOOLEAN
  tipo_treino        TEXT
  tempo_treino       INT     -- em minutos
  calorias           INT
  bike_km            FLOAT
  hora_cafe          TIME
  hora_almoco        TIME
  hora_jantar        TIME
  lazer_horas        FLOAT
  tipo_lazer         TEXT
  energia_dia        INT     -- 1 a 5

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

# 📅 Registro Diário

  data:

  hora_dormir:          hora_acordar:         sono_horas:

  estudo_horas:         conteudo_estudo:      dificuldade_estudo:

  academia:             tipo_treino:          tempo_treino:
  calorias:             bike_km:

  hora_cafe:            hora_almoco:          hora_jantar:

  lazer_horas:          tipo_lazer:

  energia_dia:
```
