# GestaoFrota-1
Exercício Prático - Sistema de Gestão de Frotas.pdf
public class Veiculo {
    String placa;
    String modelo;
    double capacidadeTanque;
    double nivelCombustivel;
    double quilometragem;

    public Veiculo(String placa, String modelo, double capacidadeTanque) {
        this.placa = placa;
        this.modelo = modelo;
        this.capacidadeTanque = capacidadeTanque;
        this.nivelCombustivel = 0.0;
        this.quilometragem = 0.0;
    }

    public void abastecer(double litros) {
        if (litros > 0) {
            double espacoDisponivel = capacidadeTanque - nivelCombustivel;
            if (litros <= espacoDisponivel) {
                nivelCombustivel += litros;
                System.out.println("Veículo " + this.placa + " abastecido com " + litros + " litros. Nível atual: " + String.format("%.2f", nivelCombustivel) + " litros.");
            } else {
                double litrosParaCompletar = espacoDisponivel;
                nivelCombustivel = capacidadeTanque;
                System.out.println("Veículo " + this.placa + " abastecido com " + String.format("%.2f", litrosParaCompletar) + " litros (tanque cheio). Nível atual: " + String.format("%.2f", nivelCombustivel) + " litros.");
            }
        } else {
            System.out.println("Quantidade de litros para abastecer deve ser positiva.");
        }
    }

    public void viajar(double distanciaKm, double consumoMedioKmPorLitro) {
        if (distanciaKm <= 0 || consumoMedioKmPorLitro <= 0) {
            System.out.println("Distância e consumo médio devem ser valores positivos.");
            return;
        }

        double litrosNecessarios = distanciaKm / consumoMedioKmPorLitro;

        if (nivelCombustivel >= litrosNecessarios) {
            nivelCombustivel -= litrosNecessarios;
            quilometragem += distanciaKm;
            System.out.println("Veículo " + this.placa + " viajou " + distanciaKm + " km. Consumo: " + String.format("%.2f", litrosNecessarios) + " litros. Quilometragem total: " + String.format("%.2f", quilometragem) + " km.");
        } else {
            System.out.println("Combustível insuficiente para viajar " + distanciaKm + " km no veículo " + this.placa + ". Litros necessários: " + String.format("%.2f", litrosNecessarios) + ", disponível: " + String.format("%.2f", nivelCombustivel) + ".");
        }
    }

    public void exibirStatus() {
        System.out.println("\n--- Status do Veículo ---");
        System.out.println("Placa: " + placa);
        System.out.println("Modelo: " + modelo);
        System.out.println("Quilometragem Total: " + String.format("%.2f", quilometragem) + " km");
        System.out.println("Combustível Restante: " + String.format("%.2f", nivelCombustivel) + " litros");
        System.out.println("------------------------");
    }
}

public class Main {
    public static void main(String[] args) {
        // 1. Instanciar dois objetos da classe Veiculo
        Veiculo van = new Veiculo("ABC-1234", "Van de Carga", 80.0);
        Veiculo caminhao = new Veiculo("XYZ-5678", "Caminhão Baú", 300.0);

        // 2. Fazer o abastecimento de ambos os veículos
        van.abastecer(50.0);
        caminhao.abastecer(200.0);

        // 3. Executar o método viajar para a Van
        van.viajar(150.0, 10.0);

        // 4. Executar o método viajar para o Caminhão
        caminhao.viajar(400.0, 4.0);

        // 5. Chamar o método exibirStatus() para os dois veículos
        van.exibirStatus();
        caminhao.exibirStatus();
    }
}
