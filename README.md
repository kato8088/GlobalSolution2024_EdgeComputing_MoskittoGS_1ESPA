# FIAP - Global Solution 2024 - Edge Computing - Grupo Moskitto GS (1ESPA)

## Membros do Grupo:
- [**Gabriel Kato**](https://github.com/kato8088) - RM560000
- [**Gabriel Couto**](https://github.com/rouri404) - RM559579
- [**João Vitor**](https://github.com/joaomatosq) - RM559246

## Descrição do Projeto:
Projeto criado para a Global Solution da FIAP de 2024, que tem como foco as energias limpas e renováveis, para um futuro mais sustentável. <br>

Quanto a isso, o nosso projeto visa descomplicar e popularizar o uso de energia solar, uma das maiores fontes de Energia Verde, não somente em grande escala, mas para usos comuns e pequenos, como carregar um aparelho ou ligar algumas luzes, por exemplo. <br>

Temos como objetivo solucionar um dos maiores problemas com a implementação de energia solar, a inacessibilidade de equipamentos caros e difíceis de encontrar para executar tarefas que outros equipamentos muito mais simples e acessíveis poderiam cumprir. <br>

No caso, criamos um monitor/gerenciador de produção de energia pelas células solares usando apenas um Arduino Uno R3, células fotovoltaicas e um display 16x2 para a fácil visualização das medições. A montagem é simples e o projeto utiliza poucos componentes externos, o que facilita a montagem e implementação em casas ou prédios por pessoas não especializadas, o que amplia considerávelmente o alcance dessa tecnologia.

## Componentes Utilizados:
- **Arduino Uno R3**
- **Tela LCD 16x2** com **Conversor Serial I2C**
- **Célula Solar**: Capacidade de geração **máxima** de 5 volts (cada)
- **Voltímetro externo para conferir a precisão do equipamento** _(opcional)_
- **Fiação apropriada**

## Informações Importantes:
Antes de começar a montagem do projeto, deve-se prestar atenção em alguns detalhes:
- Os voltímetros/multímetros presentes na imagem de exemplo da montagem **não** são obrigatórios para o projeto e **não** deverão estar no circuito após a montagem, eles servem apenas para validar a medição de voltagem do Arduino.
- Dependendo da placa utilizada, é possível adicionar mais (ou menos) células solares conforme a disponibilidade de portas GPIO analógicas.
- Preste muita atenção ao alterar ou adicionar células solares nas placas de desenvolvimento, pois nem todas as portas GPIO analógicas estão completamente disponíveis, por exemplo, no Arduino Uno R3, as portas A4 (SDA) e A5 (SCL) são utilizadas para comunicação I2C.

## Instalação e Utilização:
1. Conecte o Arduino Uno R3 em um computador com o software _Arduino IDE_ instalado.
2. Selecione a placa e porta serial correspondentes ao seu hardware (_Select Board_).
3. Instale a biblioteca [LiquidCrystal_I2C](https://reference.arduino.cc/reference/en/libraries/liquidcrystal-i2c/) e a [LiquidCrystal](https://docs.arduino.cc/libraries/liquidcrystal/) pelo gerenciador de bibliotecas integrado ao _Arduino IDE_.
4. Copie o [código fonte](https://github.com/kato8088/GlobalSolution2024_EdgeComputing_MoskittoGS_1ESPA/blob/main/GlobalSolution2024_ArduinoR3_mainSource.cpp) e cole na interface de desenvolvimento.
5. Compile e envie (_Verify & Upload_) o programa para a placa Arduino.
6. Após a conclusão do processo, desconecte o Arduino do computador e a placa estará programada corretamente.
7. Monte os componentes na placa (use o esquema fornecido de exemplo como base para a montagem).
8. Pronto!

## Funcionamento e Detalhes Técnicos:
O programa inicia, após as declarações da biblioteca _LiquidCrystal_I2C_ e a configuração do display, inicializando a comunicação serial com uma taxa de 9600 baud (bits/seg.), inicializando a comunicação com o display e o módulo I2C, ligando a luz de fundo do display e rodando a função <code>splashScreen()</code> que mostra a animação de _boot_ do nosso grupo.

Após a rotina de _setup_, a rotina de _loop_ permanece chamando a função <code>medicaoVoltagem()</code> com o ID da célula solar, que realiza a medição a cada dois segundos.

A medição da voltagem é feita pelo conversor ADC (_Analog to Digital Converter_) integrado no microcontrolador Atmel ATmega328P presente na placa de desenvolvimento Arduino Uno R3, facilitando a montagem por não usar componentes externos para a medição, porém com o lado negativo de não poder medir voltagens com precisão acima de 5V.

O ID da placa (variável _idPlaca_ recebida pela função _medicaoVoltagem()_) é determinada pelo número da porta I/O analógica (por exemplo, A0 = idPlaca é 0, A1 = idPlaca é 1).
