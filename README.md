- 👋 Hi, I’m @Jacebot23
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
import com.github.javajavalibrary.WhatsappAPI;
import com.google.zxing.WriterException;
import com.google.zxing.qrcode.QRCodeWriter;
import com.google.zxing.client.j2se.MatrixToImageWriter;

import java.io.ByteArrayOutputStream;
import java.io.IOException;
import java.net.URISyntaxException;
import java.util.Base64;
import java.util.Scanner;

import org.eclipse.jetty.server.Server;
import org.eclipse.jetty.servlet.ServletHandler;

public class Main {
    public static void main(String[] args) throws IOException, URISyntaxException {
        Scanner scanner = new Scanner(System.in);

        // Générer le QR code
        System.out.println("Hinata md bot:");
        String botName = scanner.nextLine();
        QRCodeWriter qrCodeWriter = new QRCodeWriter();
        String text = "QR code for " + botName;
        ByteArrayOutputStream stream = new ByteArrayOutputStream();
        try {
            MatrixToImageWriter.writeToStream(qrCodeWriter.encode(text), "PNG", stream);
        } catch (WriterException e) {
            e.printStackTrace();
        }
        String qrCode = Base64.getEncoder().encodeToString(stream.toByteArray());
        System.out.println("QR code generated");

        // Déployer le serveur
        Server server = new Server(Integer.parseInt(System.getenv("PORT")));
        ServletHandler handler = new ServletHandler();
        handler.addServletWithMapping(QRServlet.class, "/qr");
        server.setHandler(handler);
        try {
            server.start();
        } catch (Exception e) {
            e.printStackTrace();
        }

        // Envoyer un message WhatsApp
        WhatsappAPI whatsappAPI = new WhatsappAPI();
        System.out.println("+237693538738:");
        String recipient = scanner.nextLine();
        System.out.println("bonjour je suis Hinata bot un bot développer par la team jace est limule merci de nous avoir choisi");
        String message = scanner.nextLine();
        whatsappAPI.sendMessage(recipient, message);
        System.out.println("Message sent successfully!");
    }
}
<!---
Jacebot23/Jacebot23 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
