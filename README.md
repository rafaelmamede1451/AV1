# AV1
using System;

public abstract class CanalComunicacao
{
    public string NomeCanal { get; protected set; }

    public CanalComunicacao(string nomeCanal)
    {
        NomeCanal = nomeCanal;
    }

       public abstract void EnviarMensagem(Mensagem mensagem);
}

public abstract class Mensagem
{
    public string Conteudo { get; private set; }
    public DateTime DataEnvio { get; private set; }

    public Mensagem(string conteudo)
    {
        Conteudo = conteudo;
        DataEnvio = DateTime.Now;
    }

   
    public abstract string GetDetalhes();
}


public class WhatsApp : CanalComunicacao
{
    private string _numeroTelefone;

    public WhatsApp(string numeroTelefone) : base("WhatsApp")
    {
        _numeroTelefone = numeroTelefone;
    }

    public override void EnviarMensagem(Mensagem mensagem)
    {
        Console.WriteLine($"Enviando para o {NomeCanal} (Número: {_numeroTelefone}):");
        Console.WriteLine($"  Tipo: {mensagem.GetType().Name}");
        Console.WriteLine($"  Conteúdo: \"{mensagem.Conteudo}\"");
        Console.WriteLine($"  Detalhes: {mensagem.GetDetalhes()}");
        Console.WriteLine($"  Data de Envio: {mensagem.DataEnvio}");
        Console.WriteLine("-------------------------------------");
    }
}


public class Telegram : CanalComunicacao
{
    private string _numeroTelefone;

    public Telegram(string numeroTelefone) : base("Telegram")
    {
        _numeroTelefone = numeroTelefone;
    }

    public override void EnviarMensagem(Mensagem mensagem)
    {
        Console.WriteLine($"Enviando para o {NomeCanal} (Número: {_numeroTelefone}):");
        Console.WriteLine($"  Tipo: {mensagem.GetType().Name}");
        Console.WriteLine($"  Conteúdo: \"{mensagem.Conteudo}\"");
        Console.WriteLine($"  Detalhes: {mensagem.GetDetalhes()}");
        Console.WriteLine($"  Data de Envio: {mensagem.DataEnvio}");
        Console.WriteLine("-------------------------------------");
    }
}


public class TelegramComUsuario : CanalComunicacao
{
    private string _nomeUsuario;

    public TelegramComUsuario(string nomeUsuario) : base("Telegram")
    {
        _nomeUsuario = nomeUsuario;
    }

    public override void EnviarMensagem(Mensagem mensagem)
    {
        Console.WriteLine($"Enviando para o {NomeCanal} (Usuário: {_nomeUsuario}):");
        Console.WriteLine($"  Tipo: {mensagem.GetType().Name}");
        Console.WriteLine($"  Conteúdo: \"{mensagem.Conteudo}\"");
        Console.WriteLine($"  Detalhes: {mensagem.GetDetalhes()}");
        Console.WriteLine($"  Data de Envio: {mensagem.DataEnvio}");
        Console.WriteLine("-------------------------------------");
    }
}


public class Facebook : CanalComunicacao
{
    private string _nomeUsuario;

    public Facebook(string nomeUsuario) : base("Facebook")
    {
        _nomeUsuario = nomeUsuario;
    }

    public override void EnviarMensagem(Mensagem mensagem)
    {
        Console.WriteLine($"Enviando para o {NomeCanal} (Usuário: {_nomeUsuario}):");
        Console.WriteLine($"  Tipo: {mensagem.GetType().Name}");
        Console.WriteLine($"  Conteúdo: \"{mensagem.Conteudo}\"");
        Console.WriteLine($"  Detalhes: {mensagem.GetDetalhes()}");
        Console.WriteLine($"  Data de Envio: {mensagem.DataEnvio}");
        Console.WriteLine("-------------------------------------");
    }
}


public class Instagram : CanalComunicacao
{
    private string _nomeUsuario;

    public Instagram(string nomeUsuario) : base("Instagram")
    {
        _nomeUsuario = nomeUsuario;
    }

    public override void EnviarMensagem(Mensagem mensagem)
    {
        Console.WriteLine($"Enviando para o {NomeCanal} (Usuário: {_nomeUsuario}):");
        Console.WriteLine($"  Tipo: {mensagem.GetType().Name}");
        Console.WriteLine($"  Conteúdo: \"{mensagem.Conteudo}\"");
        Console.WriteLine($"  Detalhes: {mensagem.GetDetalhes()}");
        Console.WriteLine($"  Data de Envio: {mensagem.DataEnvio}");
        Console.WriteLine("-------------------------------------");
    }
}

public class MensagemTexto : Mensagem
{
    public MensagemTexto(string conteudo) : base(conteudo) { }

    public override string GetDetalhes()
    {
        return "Nenhum detalhe adicional para mensagem de texto.";
    }
}

public class MensagemVideo : Mensagem
{
    public string Arquivo { get; private set; }
    public string Formato { get; private set; }
    public TimeSpan Duracao { get; private set; }

    public MensagemVideo(string conteudo, string arquivo, string formato, TimeSpan duracao)
        : base(conteudo)
    {
        Arquivo = arquivo;
        Formato = formato;
        Duracao = duracao;
    }

    public override string GetDetalhes()
    {
        return $"Arquivo: {Arquivo}, Formato: {Formato}, Duração: {Duracao}";
    }
}

public class MensagemFoto : Mensagem
{
    public string Arquivo { get; private set; }
    public string Formato { get; private set; }

    public MensagemFoto(string conteudo, string arquivo, string formato)
        : base(conteudo)
    {
        Arquivo = arquivo;
        Formato = formato;
    }

    public override string GetDetalhes()
    {
        return $"Arquivo: {Arquivo}, Formato: {Formato}";
    }
}

public class MensagemArquivo : Mensagem
{
    public string Arquivo { get; private set; }
    public string Formato { get; private set; }

    public MensagemArquivo(string conteudo, string arquivo, string formato)
        : base(conteudo)
    {
        Arquivo = arquivo;
        Formato = formato;
    }

    public override string GetDetalhes()
    {
        return $"Arquivo: {Arquivo}, Formato: {Formato}";
    }
}


public class Program
{
    public static void Main(string[] args)
    {
        
        CanalComunicacao whatsapp = new WhatsApp("5511999998888");
        CanalComunicacao telegramPorTelefone = new Telegram("5511977776666");
        CanalComunicacao telegramPorUsuario = new TelegramComUsuario("@pedro_chatbot");
        CanalComunicacao facebook = new Facebook("pedro.chatbot.oficial");
        CanalComunicacao instagram = new Instagram("pedro.chatbot");

        
        MensagemTexto msgTexto = new MensagemTexto("Olá, esta é uma mensagem de texto!");
        MensagemVideo msgVideo = new MensagemVideo("Confira nosso novo vídeo!", "video_promo.mp4", "MP4", TimeSpan.FromMinutes(2.5));
        MensagemFoto msgFoto = new MensagemFoto("Nova imagem do produto.", "produto_novo.jpg", "JPEG");
        MensagemArquivo msgArquivo = new MensagemArquivo("Download do nosso e-book.", "ebook.pdf", "PDF");

        Console.WriteLine("--- SIMULAÇÃO DE ENVIO DE MENSAGENS ---");
        Console.WriteLine();

        
        whatsapp.EnviarMensagem(msgTexto);
        telegramPorTelefone.EnviarMensagem(msgVideo);
        telegramPorUsuario.EnviarMensagem(msgFoto);
        facebook.EnviarMensagem(msgArquivo);
        instagram.EnviarMensagem(msgTexto);
        whatsapp.EnviarMensagem(msgFoto);
        facebook.EnviarMensagem(msgVideo);

        Console.WriteLine("--- FIM DA SIMULAÇÃO ---");
    }
}
