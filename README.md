!apt-get install -y graphviz > /dev/null
!pip install graphviz > /dev/null

import matplotlib.pyplot as plt
import matplotlib.patches as patches
import numpy as np
import graphviz
import os
from math import pi
from google.colab import files

out_dir = "gambar_tesis_lengkap"
os.makedirs(out_dir, exist_ok=True)

def set_style():
    plt.style.use('default')
    plt.rcParams['font.family'] = 'serif'
    plt.rcParams['font.size'] = 11

# =======================================================
# 1. Gambar 2.1: Ilustrasi Presisi HBB vs OBB
# =======================================================
set_style()
fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(10, 5))
fig.suptitle('Ilustrasi Perbandingan Horizontal vs Oriented Bounding Box (Objek Berdempetan)', fontsize=14, fontweight='bold', y=1.05)

def draw_objects(ax):
    obj1 = patches.Ellipse((0.4, 0.5), 0.2, 0.6, angle=-30, edgecolor='black', facecolor='lightgray', lw=2)
    obj2 = patches.Ellipse((0.6, 0.5), 0.2, 0.6, angle=30, edgecolor='black', facecolor='darkgray', lw=2)
    ax.add_patch(obj1)
    ax.add_patch(obj2)
    ax.set_xlim(0, 1)
    ax.set_ylim(0, 1)
    ax.axis('off')

# HBB
draw_objects(ax1)
ax1.add_patch(patches.Rectangle((0.15, 0.2), 0.5, 0.6, linewidth=2, edgecolor='red', facecolor='none', linestyle='--'))
ax1.add_patch(patches.Rectangle((0.35, 0.2), 0.5, 0.6, linewidth=2, edgecolor='blue', facecolor='none', linestyle='--'))
ax1.add_patch(patches.Rectangle((0.35, 0.2), 0.3, 0.6, linewidth=0, facecolor='red', alpha=0.3)) # Area Overlap
ax1.set_title('Horizontal Bounding Box (HBB)\nOverlap Tinggi -> Salah hapus (NMS fail)', color='darkred', pad=10)

# OBB
draw_objects(ax2)
ax2.add_patch(patches.Rectangle((0.18, 0.4), 0.2, 0.62, angle=-30, linewidth=2, edgecolor='green', facecolor='none'))
ax2.add_patch(patches.Rectangle((0.5, 0.3), 0.2, 0.62, angle=30, linewidth=2, edgecolor='purple', facecolor='none'))
ax2.set_title('Oriented Bounding Box (OBB)\nOverlap Minimal -> Deteksi presisi', color='darkgreen', pad=10)
plt.tight_layout()
plt.savefig(f'{out_dir}/Gambar_2_1_HBB_vs_OBB.png', dpi=300, bbox_inches='tight')
plt.close()

# =======================================================
# 2. Flowchart & Arsitektur (Graphviz)
# =======================================================
dot_flow = graphviz.Digraph(format='png')
dot_flow.attr(rankdir='TB', size='6,8')
dot_flow.attr('node', shape='rect', style='filled,rounded', color='#4A90E2', fontcolor='white', fontname='Helvetica', margin='0.2')
alur = ['1. Studi Literatur & Identifikasi Masalah', '2. Pengumpulan Dataset Citra Komponen', '3. Anotasi Format OBB', 
        '4. Modifikasi Arsitektur: Penambahan Head P2', '5. Pelatihan 5 Varian Model YOLO', '6. Evaluasi Metrik Deteksi & Visual Counting', 
        '7. Konversi Format ONNX & Uji Kecepatan', '8. Analisis Hasil & Kesimpulan']
for i, step in enumerate(alur):
    dot_flow.node(str(i), step)
    if i > 0: dot_flow.edge(str(i-1), str(i))
dot_flow.render(f'{out_dir}/Gambar_3_1_Flowchart', cleanup=True)

dot_arch = graphviz.Digraph(format='png')
dot_arch.attr(rankdir='LR')
dot_arch.attr('node', shape='box', style='filled', fontname='Helvetica')
dot_arch.node('Input', 'Input Image\n(640x640)', fillcolor='lightgrey')
dot_arch.node('Backbone', 'Backbone\n(Ekstraksi Fitur)', fillcolor='#ffcccb')
dot_arch.node('Neck', 'Neck (PANet)\n(Fusi Skala)', fillcolor='#ffe4b5')
with dot_arch.subgraph(name='cluster_head') as c:
    c.attr(label='Modifikasi Detection Head', color='blue', style='dashed')
    c.node('P2', 'Head P2\nStride 4 (160x160)\nOptimasi Objek Sangat Kecil', fillcolor='#90ee90')
    c.node('P3', 'Head P3\nStride 8 (80x80)\nObjek Kecil', fillcolor='#add8e6')
    c.node('P4', 'Head P4\nStride 16 (40x40)\nObjek Menengah', fillcolor='#add8e6')
dot_arch.edges([('Input', 'Backbone'), ('Backbone', 'Neck')])
dot_arch.edge('Neck', 'P2', label=' Resolusi Tinggi')
dot_arch.edge('Neck', 'P3')
dot_arch.edge('Neck', 'P4')
dot_arch.render(f'{out_dir}/Gambar_2_2_Arsitektur_P2', cleanup=True)

# Desain Eksperimen (Gambar 3.2)
dot_exp = graphviz.Digraph(format='png')
dot_exp.attr(rankdir='LR')
dot_exp.attr('node', shape='box', style='filled', color='lightyellow')
dot_exp.node('D', 'Dataset 1000 Citra\n(80:10:10)')
dot_exp.node('M1', 'YOLO11n-OBB-P2\n(Proposed)', fillcolor='lightgreen')
dot_exp.node('M2', 'YOLO11n-OBB')
dot_exp.node('M3', 'YOLOv8n-OBB')
dot_exp.node('M4', 'YOLO11s-OBB')
dot_exp.node('M5', 'YOLO11n-HBB\n(Ablation)', fillcolor='#ffcccb')
dot_exp.node('E', 'Evaluasi:\n- mAP\n- MAE & Acc\n- Kecepatan', shape='cylinder', fillcolor='lightblue')
for m in ['M1','M2','M3','M4','M5']:
    dot_exp.edge('D', m)
    dot_exp.edge(m, 'E')
dot_exp.render(f'{out_dir}/Gambar_3_2_Desain_Eksperimen', cleanup=True)

# =======================================================
# 3. Grafik Hasil Evaluasi
# =======================================================
models = ['YOLOv8n-OBB', 'YOLO11n-OBB', 'YOLO11n-OBB-P2', 'YOLO11s-OBB', 'YOLO11n-HBB']
colors = ['#4A90E2', '#50E3C2', '#F5A623', '#D0021B', '#8B572A']
mAP50_95 = [0.9544, 0.9509, 0.9361, 0.9529, 0.7740]
mae = [0.29, 0.36, 0.25, 0.33, 1.67]

# Bar mAP
plt.figure(figsize=(9, 5))
bars = plt.bar(models, mAP50_95, color=colors)
plt.title('Perbandingan mAP@0.5:0.95 (Metrik Deteksi)', fontsize=14, fontweight='bold')
plt.ylabel('Nilai mAP')
plt.ylim(0.7, 1.0)
for bar in bars: plt.text(bar.get_x() + bar.get_width()/2, bar.get_height() + 0.005, f'{bar.get_height():.4f}', ha='center')
plt.grid(axis='y', linestyle='--', alpha=0.5)
plt.savefig(f'{out_dir}/Gambar_4_3_mAP.png', dpi=300, bbox_inches='tight')
plt.close()

# Radar Chart
categories = ['mAP@50-95', 'Akurasi Counting', 'Kecepatan GPU', 'Efisiensi Parameter', 'Low Error (MAE)']
N = len(categories)
data_p2      = [0.93, 0.99, 0.9, 1.0, 1.0] # P2 unggul
data_yolo11n = [0.95, 0.99, 0.95, 0.8, 0.75]
data_hbb     = [0.77, 0.97, 0.95, 0.8, 0.1]
angles = [n / float(N) * 2 * pi for n in range(N)]
angles += angles[:1]
fig, ax = plt.subplots(figsize=(7, 7), subplot_kw=dict(polar=True))
ax.set_theta_offset(pi / 2)
ax.set_theta_direction(-1)
plt.xticks(angles[:-1], categories, size=10)
def add_radar(data, color, label):
    data += data[:1]
    ax.plot(angles, data, color=color, linewidth=2, label=label)
    ax.fill(angles, data, color=color, alpha=0.1)
add_radar(data_p2, '#F5A623', 'YOLO11n-OBB-P2 (Usulan)')
add_radar(data_yolo11n, '#50E3C2', 'YOLO11n-OBB (Standar)')
add_radar(data_hbb, '#8B572A', 'YOLO11n-HBB (Baseline)')
plt.legend(loc='upper right', bbox_to_anchor=(1.3, 1.1))
plt.title('Radar Chart Evaluasi Komprehensif', size=14, fontweight='bold', y=1.1)
plt.savefig(f'{out_dir}/Gambar_4_4_Radar.png', dpi=300, bbox_inches='tight')
plt.close()

# Bar MAE
plt.figure(figsize=(9, 5))
bars = plt.bar(models, mae, color=colors)
plt.title('Perbandingan MAE (Error Penghitungan, Lebih Rendah = Baik)', fontsize=14, fontweight='bold')
plt.ylabel('MAE (Selisih Objek)')
for bar in bars: plt.text(bar.get_x() + bar.get_width()/2, bar.get_height() + 0.05, f'{bar.get_height():.2f}', ha='center', fontweight='bold')
plt.grid(axis='y', linestyle='--', alpha=0.5)
plt.savefig(f'{out_dir}/Gambar_4_5_MAE.png', dpi=300, bbox_inches='tight')
plt.close()

# Bar Density
x = np.arange(len(models))
plt.figure(figsize=(10, 6))
plt.bar(x - 0.2, [0.08, 0.12, 0.21, 0.17, 0.75], 0.4, label='Kepadatan Medium (11-30)', color='#5D9CEC')
plt.bar(x + 0.2, [0.36, 0.43, 0.26, 0.38, 1.96], 0.4, label='Kepadatan Tinggi (>30)', color='#ED5565')
plt.title('Performa MAE Berdasarkan Tingkat Kepadatan Objek', fontsize=14, fontweight='bold')
plt.xticks(x, models)
plt.legend()
plt.grid(axis='y', linestyle='--', alpha=0.5)
plt.savefig(f'{out_dir}/Gambar_4_7_Density.png', dpi=300, bbox_inches='tight')
plt.close()

# Bar Speed
plt.figure(figsize=(10, 6))
plt.bar(x - 0.2, [57.7, 41.9, 44.7, 50.9, 41.3], 0.4, label='PyTorch GPU (ms)', color='#4FC1E9')
plt.bar(x + 0.2, [213.2, 237.3, 372.7, 424.2, 133.3], 0.4, label='ONNX CPU (ms)', color='#FFCE54')
plt.title('Kecepatan Inferensi: PyTorch (GPU) vs ONNX (CPU)', fontsize=14, fontweight='bold')
plt.xticks(x, models)
plt.legend()
plt.grid(axis='y', linestyle='--', alpha=0.5)
plt.savefig(f'{out_dir}/Gambar_4_10_Kecepatan.png', dpi=300, bbox_inches='tight')
plt.close()

# Threshold
plt.figure(figsize=(9, 5))
plt.plot([0.05, 0.1, 0.2, 0.3, 0.45, 0.55, 0.6, 0.7, 0.8, 0.9], [0.59, 0.38, 0.26, 0.23, 0.20, 0.19, 0.19, 0.24, 1.78, 22.68], marker='s', lw=2, color='#AC92EC')
plt.title('Pengaruh Confidence Threshold Terhadap MAE (YOLO11n-OBB-P2)', fontsize=14, fontweight='bold')
plt.axvline(x=0.55, color='red', linestyle='--', label='Titik Optimal (0.55)')
plt.legend()
plt.grid(True, linestyle='--', alpha=0.5)
plt.savefig(f'{out_dir}/Gambar_4_9_Threshold.png', dpi=300, bbox_inches='tight')
plt.close()

print("Selesai! Mengunduh ZIP...")
!zip -r gambar_tesis_lengkap.zip gambar_tesis_lengkap/
files.download('gambar_tesis_lengkap.zip')
