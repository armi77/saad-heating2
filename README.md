# saadi-heating2
حاسبة ذكية لحساب إحتياج التدفئة المركزية للغرف "المساعد"صورة المشروع
<div dir="rtl" style="background: #fdfdfd; border: 1px solid #ddd; padding: 25px; border-radius: 12px; max-width: 420px; margin: 20px auto; box-shadow: 0 4px 6px rgba(0,0,0,0.1);">
    
    <h3 style="color: #2c3e50; text-align: center; border-bottom: 2px solid #e67e22; padding-bottom: 10px;">
        ⚙️ معالج حسابات التدفئة
    </h3>

    <div style="margin-top: 15px;">
        <label>📏 حجم الغرفة ($m^3$):</label>
        <input type="number" id="roomVolume" placeholder="أدخل الحجم..." style="width: 100%; padding: 10px; margin: 8px 0; border: 1px solid #ccc; border-radius: 6px;">
    </div>

    <div style="margin-top: 10px;">
        <label>🔥 العامل الحراري ($W/m^3$):</label>
        <input type="number" id="heatFactor" value="50" style="width: 100%; padding: 10px; margin: 8px 0; border: 1px solid #ccc; border-radius: 6px;">
    </div>

    <div style="margin-top: 10px;">
        <label>📦 عدد المشعات المتوفرة:</label>
        <input type="number" id="radCount" placeholder="كم عددها؟" style="width: 100%; padding: 10px; margin: 8px 0; border: 1px solid #ccc; border-radius: 6px;">
    </div>

    <div style="margin-top: 10px;">
        <label>⚡ قدرة المشع الواحد (واط):</label>
        <input type="number" id="radPower" placeholder="مثال: 2500" style="width: 100%; padding: 10px; margin: 8px 0; border: 1px solid #ccc; border-radius: 6px;">
    </div>

    <button onclick="executeLogic()" style="width: 100%; padding: 15px; background: #e67e22; color: #fff; border: none; border-radius: 8px; font-size: 18px; font-weight: bold; cursor: pointer; margin-top: 15px;">
        تفعيل الحسابات ⚡
    </button>

    <div id="outputWindow" style="margin-top: 20px; padding: 15px; border-radius: 8px; display: none; text-align: center;">
        <div id="reqVal" style="margin-bottom: 5px;"></div>
        <div id="availVal" style="margin-bottom: 10px;"></div>
        <div id="statusLabel" style="font-size: 20px; font-weight: bold;"></div>
    </div>

</div>

<script>
/** * هذه الدالة تشبه دالة void loop() في أردوينو 
 * لكنها لا تعمل إلا عند الضغط على الزر
 */
function executeLogic() {
    // 1. جلب البيانات من الواجهة (مثل قراءة الحساسات analogRead)
    const volume = parseFloat(document.getElementById('roomVolume').value);
    const factor = parseFloat(document.getElementById('heatFactor').value);
    const count = parseFloat(document.getElementById('radCount').value);
    const power = parseFloat(document.getElementById('radPower').value);

    // التحقق من وجود مدخلات صحيحة
    if (!volume || !factor || !count || !power) {
        alert("صديقي المبرمج، يرجى إدخال جميع الأرقام أولاً!");
        return;
    }

    // 2. العمليات الحسابية (The Math)
    const requiredPower = volume * factor; // القدرة المطلوبة
    const availablePower = count * power; // القدرة المتوفرة

    // 3. عرض النتائج (The Output)
    const output = document.getElementById('outputWindow');
    output.style.display = 'block';
    
    document.getElementById('reqVal').innerText = "المطلوب هندسياً: " + requiredPower + " واط";
    document.getElementById('availVal').innerText = "المتوفر حالياً: " + availablePower + " واط";

    const label = document.getElementById('statusLabel');
    if (availablePower >= requiredPower) {
        label.innerText = "النتيجة: كافية تماماً ✅";
        label.style.color = "#27ae60";
        output.style.backgroundColor = "#eafaf1";
    } else {
        label.innerText = "النتيجة: غير كافية ❌";
        label.style.color = "#c0392b";
        output.style.backgroundColor = "#fdedec";
    }
}
</script>
