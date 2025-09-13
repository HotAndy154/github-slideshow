const resetUrl = `${process.env.FRONTEND_URL}/reset-password?token=${token}&email=${encodeURIComponent(email)}`;
const currentYear = new Date().getFullYear();

const htmlTemplate = fs.readFileSync('reset-password-email.html', 'utf8')
  .replace('{{RESET_URL}}', resetUrl)
  .replace('{{CURRENT_YEAR}}', currentYear);

await transporter.sendMail({
  from: process.env.SMTP_FROM,
  to: email,
  subject: 'Restablece tu contraseña',
  html: htmlTemplate
});
