Simulado Ac2
Programa em Java para controle de estoque de uma loja. Permite cadastrar produtos, classificar o nível de estoque segundo um limite mínimo configurável, gerar relatórios com estatísticas e calcular reposições necessárias para atingir um estoque ideal informado pelo usuário. O sistema suporta múltiplos ciclos de execução (o usuário pode optar por alterar ou manter o limite mínimo entre execuções).

    public static void main(String[] args) {
        
        Scanner sc = new Scanner (System.in);
        
        int minimoItem = 0; //limite minimo de estoque
        int totalDeProdutos = 0; //numero total de produtos a serem cadastrados
        int contAdequado = 0; 
        int contCritico = 0; 
        int contBaixo = 0;
        int totalDeUnidades = 0;
        int estoqueIdeal = 0;
        int totalARepor = 0;
        
        // Passo 1 - Entrada de dados iniciais (limite mínimo de estoque)
        System.out.println("Controle de Estoque");
        System.out.println("Indique aqui o valor minimo aceitavel de cada item em estoque:");
        minimoItem = sc.nextInt();
            
            while (minimoItem < 0) {            
                System.out.println("Erro! Insira novamente (> 0):");
                minimoItem = sc.nextInt();
            }
        System.out.println("Valor minimo registrado (" + minimoItem + ") foi aceito!");
        System.out.println("--------------------------------------------");
        
        // Passo 2 - Lançamento dos produtos -> Solicitar o número total de produtos a serem cadastrados
        System.out.println("Indique o numero total de produtos a serem cadastrados:");
        totalDeProdutos = sc.nextInt();
        
            while (totalDeProdutos < 0) {            
                System.out.println("Erro! Insira novamente (> 0):");
                totalDeProdutos = sc.nextInt();
            }
            
        System.out.println("Valor minimo registrado (" + totalDeProdutos + ") foi aceito!");
        System.out.println("--------------------------------------------");
        
        //Solicitar o nome e quantidade de cada produto
        String[] nomeProdutos = new String[totalDeProdutos];
        int[] quantidade = new int[totalDeProdutos];
        String[] status = new String[totalDeProdutos];
        
        sc.nextLine();
        
        System.out.println("Indique o nome de cada produto a serem cadastrados");
            for (int nProdutos = 0; nProdutos < totalDeProdutos; nProdutos++) {
                System.out.print("Nome do produto " + (nProdutos + 1) + ": ");
                nomeProdutos[nProdutos] = sc.nextLine();
            } 
            for (int i = 0; i < totalDeProdutos; i++) {
                System.out.print("Quantidade em estoque de " + nomeProdutos[i] + ": ");
                quantidade[i] = sc.nextInt();
                
                if(quantidade[i] < 0) {
                    System.out.println("Quantidade invalida! Deve ser zero ou maior.");
                    while (quantidade [i] < 0) {                        
                        System.out.print("Quantidade em estoque de " + nomeProdutos[i] + ": ");
                        quantidade[i] = sc.nextInt();    
                    }
                }
                System.out.println("--------------------------------------------");
                
                //Classificando os produtos
                    if (quantidade[i] >= minimoItem) {
                        status[i] = "Adequado";
                        contAdequado++;
                        System.out.println("Produto: " + nomeProdutos[i]);
                        System.out.println("Quantidade: " + quantidade[i]);
                        System.out.println("Status: " + status[i]);           
                    } else if (quantidade [i] >= minimoItem/2){
                        status[i] = "Baixo";
                        contBaixo++;
                        System.out.println("Produto: " + nomeProdutos[i]);
                        System.out.println("Quantidade: " + quantidade[i]);
                        System.out.println("Status: " +status[i]);
                    } else if (quantidade [i] < minimoItem/2) {
                        status[i] = "Critico";
                        contCritico++;
                        System.out.println("Produto: " + nomeProdutos[i]);
                        System.out.println("Quantidade: " + quantidade[i]);
                        System.out.println("Status: " + status[i]);
                    }
                totalDeUnidades += quantidade[i];
                System.out.println("--------------------------------------------");
            }
            
            double percentualBaixo = contBaixo* 100/totalDeProdutos; 
            double percentualCritico = contCritico* 100/totalDeProdutos;
            double percentualAdequado = contAdequado* 100/totalDeProdutos;
                
            System.out.println("Percentual Adequado: " + percentualAdequado + "%");
            System.out.println("Percentual Baixo: " + percentualBaixo + "%");
            System.out.println("Percentual Crítico: " + percentualCritico + "%");
        
        sc.nextLine();
            
        //Relatório Geral
        System.out.println("");    
        System.out.println("Relatorio Geral de Estoque:");
            for (int i = 0; i < totalDeProdutos; i++) {
                System.out.println("Produtos: " + nomeProdutos[i] +
                                   " | Quantidade: " + quantidade[i] +
                                   " | Status: " + status[i]);
            }
            
        System.out.println("Total Geral de Unidades: " + totalDeUnidades);
        System.out.println("--------------------------------------------");
        
        //Calculo de Reposição
        System.out.println("Qual e o Estoque Ideal para cada Produto: ");
        estoqueIdeal = sc.nextInt();
            while (estoqueIdeal < 0) {            
                System.out.println("Erro! Insira novamente (deve ser maior que 0):");
                estoqueIdeal = sc.nextInt();
            }
            
        System.out.println("RELATORIO DE REPOSICAO ");
            for (int i = 0; i < totalDeProdutos; i++) {
                if (quantidade[i] < estoqueIdeal) {
                   int faltando = estoqueIdeal - quantidade[i];
                   System.out.println("Produto: " + nomeProdutos[i] + 
                                      " | Quantidade Atual:" + quantidade[i] +
                                      " | Falta repor: " + faltando + " unidades.");
                   totalARepor += faltando;
                } else {
                    System.out.println("Produto: " + nomeProdutos[i] + " | Quantidade Atual:" + quantidade[i] +
                                       " | Estoque suficiente.");
                }
            }
        
            System.out.println("--------------------------------------------");
            System.out.println("Total Geral de Unidades: " + totalDeUnidades);
            System.out.println("Total a repor: " + totalARepor);
            if (totalDeUnidades > 0) {
                double percentualReposicao = (totalARepor * 100.0) / totalDeUnidades;
                System.out.println("Percentual de reposicao: " + percentualReposicao + "%");
            } else {
                System.out.println("Percentual de reposicao: Indisponível (estoque vazio).");
            }
    }
}
