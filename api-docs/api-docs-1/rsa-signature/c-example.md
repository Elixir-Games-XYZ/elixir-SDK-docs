---
description: C# Example of RSA signature implementation with signature verify
---

# 🔢 C# Example

<pre class="language-csharp"><code class="lang-csharp">using System;
using System.IO;
using System.Net;
using System.Security.Cryptography; using System.Text;
using System.Threading.Tasks;
namespace Elixir {
public static class EndPoints {
static string baseURL = "https://kend.elixir.app";

// Verifies a signature against the signature verification endpoint
public static async Task&#x3C;string> SignatureVerify(string body) {
 try {
  // Compose URL
  WebRequest request = WebRequest.Create($"{baseURL}/sdk/v2/signature/verify"); // Use POST
  request.Method = "POST";
  // Get Epoch time in milliseconds.
  string timeStamp = (System.DateTime.UtcNow - new System.DateTime(1970, 1, 1)).TotalMilliseconds.ToString();
  // Calculate body signature
  string signature = Crypto.SignFromFile(body, timeStamp, "key.pem");
  // Set headers
  request.Headers["content-type"] = "application/json";
  request.Headers["x-api-token"] = timeStamp;
  // Public key
  request.Headers["x-api-key"] = File.ReadAllText("public.key");
  // Signature
  request.Headers["x-api-signature"] = signature;
  // Body to binary
  var data = Encoding.UTF8.GetBytes(body);
  // Set request content length.
  request.ContentLength = data.Length;
  // Write data to request.
  Stream newStream = request.GetRequestStream();
  newStream.Write(data, 0, data.Length);
  // Wait for response
  WebResponse response = await request.GetResponseAsync();
  // Read response data
  var reader = new StreamReader(response.GetResponseStream(), ASCIIEncoding.UTF8); 
  return reader.ReadToEnd();
 } catch(Exception e) { 
  return e.Message;
 }
}


internal static class Crypto {
// Sign message reading PK from file
public static string SignFromFile(string body, string timeStamp, string file) {
  return Sign(body, timeStamp, File.ReadAllText(file)); 
}
// Sign message given in body, with the given timestamp and private key
public static string Sign(string body, string timeStamp, string privateKey) {
<strong>  RSACryptoServiceProvider provider = GetRSA(privateKey);
</strong>  byte[] signature = provider.SignData(Encoding.UTF8.GetBytes($"{body}.{timeStamp}"), CryptoConfig.CreateFromName("SHA256"));
  StringBuilder hex = new StringBuilder(signature.Length * 2); 
  foreach (byte b in signature) hex.AppendFormat("{0:x2}", b); 
  return hex.ToString();
}

const string KEY_HEADER = "-----BEGIN PRIVATE KEY-----";
const string KEY_FOOTER = "-----END PRIVATE KEY-----";

internal static RSACryptoServiceProvider GetRSA(string pem) {
<strong>  string keyFormatted = pem;
</strong>  int cutIndex = keyFormatted.IndexOf(KEY_HEADER);
  keyFormatted = keyFormatted.Substring(cutIndex, keyFormatted.Length - cutIndex); 
  cutIndex = keyFormatted.IndexOf(KEY_FOOTER);
  keyFormatted = keyFormatted.Substring(0, cutIndex + KEY_FOOTER.Length); keyFormatted = keyFormatted.Replace(KEY_HEADER, "");
  keyFormatted = keyFormatted.Replace(KEY_FOOTER, "");
  keyFormatted = keyFormatted.Replace("\r", "");
  keyFormatted = keyFormatted.Replace("\n", ""); keyFormatted = keyFormatted.Trim();

  byte[] privateKeyRaw = System.Convert.FromBase64String(keyFormatted); 
  RSACryptoServiceProvider rsa = new RSACryptoServiceProvider(); 
  rsa.ImportPkcs8PrivateKey(new ReadOnlySpan&#x3C;byte>(privateKeyRaw), out _); 
return rsa;
}
</code></pre>
