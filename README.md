# aa
import { useState } from "react";
import { Button } from "@/components/ui/button";
import { Card, CardContent } from "@/components/ui/card";
import { Upload } from "lucide-react";

export default function GhibliStyleApp() {
  const [image, setImage] = useState(null);
  const [converted, setConverted] = useState(null);
  const [loading, setLoading] = useState(false);

  const handleUpload = (event) => {
    const file = event.target.files[0];
    if (file) {
      setImage(URL.createObjectURL(file));
    }
  };

  const handleConvert = async () => {
    if (!image) return;
    setLoading(true);
    // Simulate API call for conversion
    setTimeout(() => {
      setConverted(image); // Replace with actual processed image URL
      setLoading(false);
    }, 2000);
  };

  return (
    <div className="flex flex-col items-center justify-center min-h-screen p-4 bg-gray-100">
      <Card className="w-full max-w-md p-4">
        <CardContent className="flex flex-col items-center gap-4">
          <input type="file" accept="image/*" onChange={handleUpload} className="hidden" id="upload" />
          <label htmlFor="upload" className="cursor-pointer">
            <Button variant="outline">
              <Upload className="mr-2" /> رفع صورة
            </Button>
          </label>
          {image && <img src={image} alt="Uploaded" className="w-full rounded-lg" />}
          <Button onClick={handleConvert} disabled={!image || loading}>
            {loading ? "جارٍ المعالجة..." : "تحويل إلى ستايل جيبلي"}
          </Button>
          {converted && <img src={converted} alt="Converted" className="w-full rounded-lg mt-4" />}
        </CardContent>
      </Card>
    </div>
  );
}
