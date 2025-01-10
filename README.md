[import React, { useState, useEffect } from 'react';
import { 
  UserIcon, 
  PhoneIcon, 
  MapPinIcon, 
  PlusIcon, 
  XMarkIcon, 
  CheckCircleIcon 
} from '@heroicons/react/24/outline';

const ThaiChildrensDayForm = () => {
  // State declarations
  const [formData, setFormData] = useState({
    parentName: '',
    parentPhone: '',
    address: '',
    subdistrict: '',
    district: '',
    children: [],
    selectedActivities: []
  });
  
  const [isSubmitted, setIsSubmitted] = useState(false);
  const [registrationId, setRegistrationId] = useState('');
  const [errors, setErrors] = useState([]);

  // Constants
  const districts = ['เมืองขอนแก่น', 'น้ำพอง', 'กระนวน', 'เขาสวนกวาง', 'อุบลรัตน์'];

  const activities = [
    { id: 'balloon', label: '🎯 ยิงเป้าลูกโป่ง (10 คะแนน)' },
    { id: 'ball', label: '🎳 ปาลูกบอลใส่กระป๋อง (10 คะแนน)' },
    { id: 'plane', label: '✈️ พับเครื่องบินกระดาษ (10 คะแนน)' },
    { id: 'tug', label: '🏃 ชักเย่อ (20 คะแนน)' },
    { id: 'quiz', label: '❓ ตอบคำถาม (20 คะแนน)' },
    { id: 'firstaid', label: '🏥 การปฐมพยาบาลเบื้องต้น (20 คะแนน)' }
  ];

  // Add child handler
  const addChild = () => {
    setFormData(prev => ({
      ...prev,
      children: [...prev.children, { id: Date.now(), name: '', age: '' }]
    }));
  };

  // Remove child handler
  const removeChild = (childId) => {
    setFormData(prev => ({
      ...prev,
      children: prev.children.filter(child => child.id !== childId)
    }));
  };

  // Form submission handler
  const handleSubmit = async (e) => {
    e.preventDefault();
    
    // Validation
    const newErrors = [];
    if (!formData.parentName) newErrors.push('กรุณากรอกชื่อ-สกุล ผู้ปกครอง');
    if (!formData.parentPhone) newErrors.push('กรุณากรอกเบอร์โทรศัพท์');
    if (!formData.address) newErrors.push('กรุณากรอกที่อยู่');
    if (!formData.subdistrict) newErrors.push('กรุณากรอกตำบล');
    if (!formData.district) newErrors.push('กรุณาเลือกอำเภอ');
    if (formData.children.length === 0) newErrors.push('กรุณากรอกข้อมูลเด็กอย่างน้อย 1 คน');

    if (newErrors.length > 0) {
      setErrors(newErrors);
      return;
    }

    // Generate registration ID
    const newRegistrationId = Math.floor(1000 + Math.random() * 9000).toString();
    setRegistrationId(newRegistrationId);
    setIsSubmitted(true);
  };

  return (
    <div className="min-h-screen bg-gradient-to-br from-pink-100 via-purple-100 to-indigo-100 py-12 px-4 sm:px-6">
      <div className="max-w-3xl mx-auto">
        {/* Form Container */}
        <div className="bg-white/90 backdrop-blur-sm rounded-xl shadow-xl overflow-hidden">
          {/* Rainbow Gradient Border */}
          <div className="h-1 bg-gradient-to-r from-red-500 via-yellow-500 to-blue-500" />

          <div className="p-8">
            {/* Header */}
            <div className="text-center mb-8">
              <h1 className="text-3xl font-bold text-transparent bg-clip-text bg-gradient-to-r from-purple-600 to-pink-600">
                ลงทะเบียนวันเด็กแห่งชาติ
              </h1>
              <h3 className="text-gray-600 mt-2">
                ณ ศูนย์การฝึกกองทัพอากาศน้ำพอง จังหวัดขอนแก่น ปี 2568
              </h3>
            </div>

            {/* Success Message */}
            {isSubmitted ? (
              <div className="text-center p-8 bg-green-50 rounded-lg">
                <CheckCircleIcon className="h-16 w-16 text-green-500 mx-auto mb-4" />
                <h2 className="text-2xl font-semibold text-green-700 mb-4">
                  ลงทะเบียนสำเร็จ!
                </h2>
                <p className="text-lg mb-4">
                  รหัสการลงทะเบียนของคุณคือ: 
                  <span className="block text-3xl font-mono font-bold text-blue-600 my-2">
                    {registrationId}
                  </span>
                </p>
                <button
                  onClick={() => window.location.reload()}
                  className="mt-4 px-6 py-2 bg-green-600 text-white rounded-lg hover:bg-green-700 transition-colors"
                >
                  ลงทะเบียนอีกครั้ง
                </button>
              </div>
            ) : (
              /* Form Content */
              <form onSubmit={handleSubmit} className="space-y-6">
                {/* Error Messages */}
                {errors.length > 0 && (
                  <div className="bg-red-50 text-red-700 p-4 rounded-lg">
                    <h4 className="font-semibold mb-2">พบข้อผิดพลาด:</h4>
                    <ul className="list-disc pl-5">
                      {errors.map((error, index) => (
                        <li key={index}>{error}</li>
                      ))}
                    </ul>
                  </div>
                )}

                {/* Parent Information */}
                {/* ... (Continue with form fields similar to your original HTML) ... */}

                {/* Submit Button */}
                <button
                  type="submit"
                  className="w-full py-3 bg-gradient-to-r from-purple-600 to-pink-600 text-white rounded-lg font-semibold hover:from-purple-700 hover:to-pink-700 transition-all transform hover:-translate-y-0.5"
                >
                  ลงทะเบียน
                </button>
              </form>
            )}
          </div>
        </div>
      </div>
    </div>
  );
};

export default ThaiChildrensDayForm;](http://localhost:8888/children/)
