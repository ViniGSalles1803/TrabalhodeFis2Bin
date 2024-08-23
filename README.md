import javax.swing.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class ResistenciaTrilho {
    public static void main(String[] args) {
        JFrame frame = new JFrame("Cálculo da Resistência de um Trilho de Aço");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setSize(400, 250);
        
        JPanel panel = new JPanel();
        frame.add(panel);
        placeComponents(panel);
        
        frame.setVisible(true);
    }

    private static void placeComponents(JPanel panel) {
        panel.setLayout(null);

        JLabel labelAreaSecao = new JLabel("Área da Seção (cm²):");
        labelAreaSecao.setBounds(10, 20, 160, 25);
        panel.add(labelAreaSecao);

        JTextField areaSecaoText = new JTextField(20);
        areaSecaoText.setBounds(180, 20, 165, 25);
        areaSecaoText.setText("56.0"); // Valor padrão
        panel.add(areaSecaoText);

        JLabel labelComprimento = new JLabel("Comprimento (km):");
        labelComprimento.setBounds(10, 50, 160, 25);
        panel.add(labelComprimento);

        JTextField comprimentoText = new JTextField(20);
        comprimentoText.setBounds(180, 50, 165, 25);
        comprimentoText.setText("10.0"); // Valor padrão
        panel.add(comprimentoText);

        JLabel labelResistividade = new JLabel("Resistividade (Ω·m):");
        labelResistividade.setBounds(10, 80, 160, 25);
        panel.add(labelResistividade);

        JTextField resistividadeText = new JTextField(20);
        resistividadeText.setBounds(180, 80, 165, 25);
        resistividadeText.setText("3.00e-1"); // Valor padrão
        panel.add(resistividadeText);

        JButton calcularButton = new JButton("Calcular");
        calcularButton.setBounds(10, 110, 150, 25);
        panel.add(calcularButton);

        JLabel resultadoLabel = new JLabel("Resistência: ");
        resultadoLabel.setBounds(10, 140, 350, 25);
        panel.add(resultadoLabel);

        calcularButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                try {
                    double areaSecao = Double.parseDouble(areaSecaoText.getText());
                    double comprimento = Double.parseDouble(comprimentoText.getText());
                    double resistividade = Double.parseDouble(resistividadeText.getText());

                    // Convertendo a área de cm² para m²
                    double areaSecaoM2 = areaSecao * 1e-4;

                    // Convertendo o comprimento de km para metros
                    double comprimentoM = comprimento * 1e3;

                    // Calculando a resistência usando a fórmula R = ρ * L / A
                    double resistencia = (resistividade * comprimentoM) / areaSecaoM2;

                    resultadoLabel.setText(String.format("Resistência: %.4f Ω", resistencia));
                } catch (NumberFormatException ex) {
                    resultadoLabel.setText("Por favor, insira valores válidos.");
                }
            }
        });
    }
}
