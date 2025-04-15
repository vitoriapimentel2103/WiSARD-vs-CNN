🧠 Projeto de Comparação entre WiSARD e CNN no Reconhecimento de Dígitos Manuscritos (MNIST)
Esse projeto foi desenvolvido por mim, Maria Vitória Pimentel Araújo, como um experimento comparativo entre dois modelos de classificação bem diferentes: uma rede WiSARD (baseada em memória RAM) e uma CNN (rede neural convolucional clássica) para reconhecer dígitos do dataset MNIST.

🧩 Pré-processamento
Primeiro, eu carreguei o dataset MNIST usando o Keras. O MNIST é composto por imagens 28x28 de dígitos escritos à mão. Para treinar o WiSARD, transformei essas imagens em binárias, comparando cada pixel com o valor 127 (ou seja, se o pixel for maior que 127, ele vira 1, senão vira 0). Depois, achatei cada imagem 28x28 pra um vetor de 784 posições. Também mostrei uma amostrinha visual com matplotlib só pra ter certeza de que estava tudo certo com os dados.

🧠 Implementando o WiSARD
Implementei uma classe Discriminator, que funciona como o cérebro da rede WiSARD. Cada discriminador é responsável por aprender a reconhecer um dígito específico (0 a 9). A entrada binária é dividida em vários endereços menores (RAMs), que guardam os padrões que aparecem durante o treino. Usei um embaralhamento aleatório fixo pra criar o mapeamento (chamado de shared mapping), o que ajuda a garantir que todos os discriminadores usem os mesmos padrões de divisão dos dados.

⚙️ Treinamento do WiSARD
Criei 10 discriminadores (um pra cada classe de dígito) e treinei cada um apenas com as imagens da sua respectiva classe. O treino é super rápido, porque o WiSARD basicamente só conta quantas vezes cada padrão aparece.

🔍 Predição com WiSARD
Na hora de testar, pra cada imagem eu passo por todos os discriminadores e vejo qual responde melhor (ou seja, qual RAM tem mais padrões que batem com a entrada). Implementei um sistema de bleaching, que resolve empates tentando ir diminuindo o nível de exigência até sobrar só um candidato. No final, calculei a acurácia do WiSARD no conjunto de teste e o tempo total de inferência.

🧠 Implementando a CNN
Pra comparar com um modelo mais tradicional e robusto, também treinei uma CNN simples usando PyTorch. Ela tem duas camadas convolucionais + pooling, depois duas camadas totalmente conectadas. Usei ReLU como função de ativação e Adam como otimizador. O treino foi feito por 3 épocas com batch size de 64, e os dados foram normalizados automaticamente com ToTensor().

📊 Comparação entre modelos
Ao final, comparei os dois modelos tanto em tempo de treinamento quanto em acurácia. A CNN, como esperado, tem uma acurácia bem maior — mas também é bem mais pesada pra treinar. Já o WiSARD é super leve e rápido, o que pode ser uma vantagem dependendo do contexto. A ideia aqui não é dizer qual é "melhor", mas mostrar como diferentes abordagens funcionam pra o mesmo problema.
