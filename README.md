# Estrutura-For
Exercícios passados em aula para treinar o uso da estrutura FOR 

//Crie um algoritmo que imprima os números de 10 a 1 em ordem decrescente.

public static void main(String[] args) {
       
        System.out.println("Vamos contar de 10 ate o 1?");
        System.out.println("A forma correta e:");
        
        // for [inicialização(condição inicial necessaria); condição (ate onde vai ser contado); incremento ou decremento;] 
        for (int number = 10; number >= 1; number--) {
            System.out.println(number);    
        }
  }
