import java.util.Scanner;

public class ImpostoDeRenda {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Informe a renda anual com salário: ");
        double salarioAnual = scanner.nextDouble();
        System.out.print("Informe a renda anual com prestação de serviços: ");
        double rendaServicos = scanner.nextDouble();
        System.out.print("Informe o ganho de capital anual: ");
        double ganhoCapital = scanner.nextDouble();
        System.out.print("Informe os gastos anuais com saúde e educação: ");
        double gastosSaudeEducacao = scanner.nextDouble();

        String relatorio = calcularImpostoRenda(salarioAnual, rendaServicos, ganhoCapital, gastosSaudeEducacao);
        System.out.println(relatorio);
    }

    public static String calcularImpostoRenda(double salarioAnual, double rendaServicos, double ganhoCapital, double gastosSaudeEducacao) {
       
        double salarioMensal = salarioAnual / 12;
        double impostoSalario = 0;
        if (salarioMensal < 3000) {
            impostoSalario = 0;
        } else if (salarioMensal < 5000) {
            impostoSalario = salarioMensal * 0.1;
        } else {
            impostoSalario = salarioMensal * 0.2;
        }

       
        double impostoServicos = rendaServicos * 0.15;
        double impostoCapital = ganhoCapital * 0.2;

        double impostoBruto = impostoSalario + impostoServicos + impostoCapital;

    
        double abatimentoMaximo = impostoBruto * 0.3;
        double abatimento = Math.min(abatimentoMaximo, gastosSaudeEducacao);

       
        double impostoPagar = impostoBruto - abatimento;

        String relatorio = """
                Relatório de Imposto de Renda

                Renda Anual com Salário: R$ %.2f
                Renda Anual com Serviços: R$ %.2f
                Ganho de Capital Anual: R$ %.2f
                Gastos com Saúde e Educação: R$ %.2f

                Imposto sobre Salário: R$ %.2f
                Imposto sobre Serviços: R$ %.2f
                Imposto sobre Capital: R$ %.2f

                Imposto Bruto: R$ %.2f
                Abatimento: R$ %.2f

                Imposto a Pagar: R$ %.2f
                """
                .formatted(salarioAnual, rendaServicos, ganhoCapital, gastosSaudeEducacao,
                        impostoSalario, impostoServicos, impostoCapital,
                        impostoBruto, abatimento, impostoPagar);
        return relatorio;
    }
}
