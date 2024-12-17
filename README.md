<?php
// Handle report form submission
if ($_SERVER['REQUEST_METHOD'] === 'POST' && isset($_POST['report'])) {
    // Process report form submission
    $incident_type = $_POST['incident_type'];
    $description = $_POST['description'];
    $attachments = $_FILES['attachments'];

    // Example of handling file upload
    $uploaded_files = [];
    if ($attachments['error'][0] === 0) {
        foreach ($attachments['tmp_name'] as $key => $tmp_name) {
            $file_name = $attachments['name'][$key];
            $file_path = 'uploads/' . $file_name;
            if (move_uploaded_file($tmp_name, $file_path)) {
                $uploaded_files[] = $file_path;
            }
        }
    }

    // Store the report data or send an email, etc.
    // For now, just echo the data
    echo "Report submitted: Incident Type - $incident_type, Description - $description";
    // Store or process the data as required (save to DB, email, etc.)
}

// Handle appointment form submission
if ($_SERVER['REQUEST_METHOD'] === 'POST' && isset($_POST['appointment'])) {
    $name = $_POST['name'];
    $email = $_POST['email'];
    $preferred_date = $_POST['preferred_date'];
    $message = $_POST['message'];

    // Store or send appointment data (store in DB, send email, etc.)
    echo "Appointment booked: Name - $name, Email - $email, Date - $preferred_date, Message - $message";
    // Add appropriate backend code to store data or send confirmation email
}
?>
