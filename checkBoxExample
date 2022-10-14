import sys
from PySide2 import QtWidgets
from PySide2 import QtCore
import maya.OpenMayaUI as omui
from shiboken2 import wrapInstance
import maya.cmds as mc

mc.ls("lod*")

def get_maya_window():
    """
    Return the Maya main window widget as a Python object
    """
    main_window_ptr = omui.MQtUtil.mainWindow()
    if sys.version_info.major >= 3:
        return wrapInstance(int(main_window_ptr), QtWidgets.QWidget)
    else:
        return wrapInstance(long(main_window_ptr), QtWidgets.QWidget)


class LodExporterUI(QtWidgets.QMainWindow):

    def __init__(self, debug=False, *args, **kwargs):
        """
        This si the main window which will called to open UI
        :param args:
        :param kwargs:
        :param debug : debug
        """
        super(LodExporterUI, self).__init__(get_maya_window(), *args, **kwargs)
        
        self.main_ly = QtWidgets.QVBoxLayout()
        
        self.kaka_btn = QtWidgets.QPushButton("kaka")
        
        self.kaka_btn.clicked.connect(self.export_fbs)
        self.q_w = QtWidgets.QWidget()
        self.q_w.setLayout(self.main_ly)
        self.main_ly.addWidget(self.kaka_btn)
        self.setCentralWidget(self.q_w)
        self.checks = dict()
        
        self.get_lods()
        
    
    def get_lods(self):
        
        lods = [x for x in mc.ls("lod*") if mc.nodeType(x) == "transform"]
        for i in lods:
            check = QtWidgets.QCheckBox(i)
            self.checks[i] = check
            self.main_ly.addWidget(check)
        
    
    def export_fbs(self):

        for i,j in self.checks.items():
            if mc.ls(i):
                if j.checkState() == QtCore.Qt.CheckState.Checked:
                    print "exporting {}".format(i)
        


obj = LodExporterUI()

obj.show()
